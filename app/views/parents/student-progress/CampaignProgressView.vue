<template>
  <div
    v-if="campaign"
    class="campaign-progress"
  >
    <module-progress-data-component
      :levels="sortedLevels"
      :level-sessions="levelSessions"
    />
    <module-resources
      :campaign="campaign"
    />
  </div>
</template>

<script>
import ModuleProgressDataComponent from './ModuleProgressDataComponent'
import ModuleResources from './ModuleResources'
export default {
  name: 'CampaignProgressView',
  props: {
    campaign: {
      type: Object
    },
    levelSessions: {
      type: Array
    },
    sortedLevels: {
      type: Array,
      default () {
        return []
      }
    }
  },
  components: {
    ModuleProgressDataComponent,
    ModuleResources
  }
}
</script>

<style scoped lang="scss">
.campaign-progress {
  display: grid;
  grid-template-columns: 2.5fr 1fr;
}
</style>
