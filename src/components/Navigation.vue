<template>
  <nav>
    <base-card>
      <div class="tabs">
        <button class="tab" :class="isActive('stored')" @click="setActive('stored')">Stored Resources</button>
        <button class="tab" :class="isActive('add')" @click="setActive('add')">Add Resource</button>
      </div>
    </base-card>
  </nav>
</template>

<script>
import BaseCard from './basecomponents/BaseCard.vue'
export default {
  components: {
    BaseCard
  },
  props: ['activeTab'],
  methods: {
    setActive(id) {
      this.$emit('change-tab', id)
    },
    isActive(id) {
      return {
        active: this.activeTab === id
      }
    }
  }
}
</script>

<style>
.tabs {
  @apply flex 
}

.tab {
  @apply text-lg py-4 px-10 mr-2 rounded-md text-purple-900 hover:bg-purple-400 hover:text-white
}

.active {
  @apply text-white bg-purple-800
}
</style>