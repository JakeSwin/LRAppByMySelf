<template>
  <div class="resources">
    <div
      v-for="resource in resources"
      :key="resource.id"
      class="resource-container"
    >
      <resource-card :info="resource" @delete-card="deleteResource"></resource-card>
    </div>
  </div>
</template>

<script>
import ResourceCard from './ResourceCard.vue'
export default {
  components: {
    ResourceCard
  },
  props: ['resources'],
  methods: {
    deleteResource(id) {
      this.$emit('delete-resource', id)
    }
  }
}
</script>