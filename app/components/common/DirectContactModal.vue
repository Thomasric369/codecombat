<script>
  import ModalDivider from 'app/components/common/ModalDivider'
  import Modal from 'app/components/common/Modal'

  export default Vue.extend({
    components: {
      ModalDivider,
      Modal
    },
    data: () => ({
    }),
    methods: {
      showError (error) {
        console.error(error)
        noty({
          text: 'Unable to load chat (may be due to browser privacy features)',
          layout: 'topCenter',
          type: 'error',
          timeout: 5000
        })
      },
      programaticallyClose () {
        // Because this modal is created from Backbone, we don't have a clean way to
        // close the modal other than interacting with data-dismiss='modal' through clicking.
        $('#coco-modal-header-close-button').click()
      },
      clickedSalesChat () {
        try {
          zE('messenger', 'open')
          this.programaticallyClose()
          window.tracker.trackEvent('Sales chat opened')
        } catch (e) {
          this.showError(e)
        }
      },
      clickedSupportChat () {
        try {
          zE('messenger', 'open')
          this.programaticallyClose()
          window.tracker.trackEvent('Support chat opened')
        } catch (e) {
          this.showError(e)
        }
      },
    }
  })
</script>

<template>
  <modal
      :backbone-dismiss-modal="true"
      :title="$t('general.contact_us')"
  >
    <div class="flex-container column">
      <p>{{ $t("general.chat_with_us") }} (9am-6pm ET)</p>
      <div class="flex-container">
        <div class="flex-container column">
          <button @click.prevent="clickedSupportChat" class="btn btn-large btn-primary btn-moon">{{ $t("general.support") }}</button>
        </div>

        <div class="flex-container column">
          <button @click.prevent="clickedSalesChat" class="btn btn-large btn-primary btn-moon">{{ $t("general.sales") }}</button>
        </div>
      </div>

      <modal-divider />

      <div>
        {{ $t('general.email_us') }}: <a href="mailto:support@codecombat.com">support@codecombat.com</a>
      </div>
    </div>
  </modal>
</template>

<style lang="scss" scoped>
@import "app/styles/style-flat-variables";
@import "app/styles/core/variables";

.flex-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}

.column {
  flex-direction: column;
}

// These types of buttons could be shared better
.btn-primary.btn-moon {
  background-color: $moon;
  border-radius: 1px;
  color: $gray;
  text-shadow: unset;
  font-weight: bold;
  @include font-h-5-button-text-black;
  min-width: 260px;
  padding: 15px 0;
  background-image: unset;
  margin: 0 15px;

  &:hover {
    @include font-h-5-button-text-white;
    background-color: $goldenlight;
    transition: background-color .35s;
  }
}
</style>
