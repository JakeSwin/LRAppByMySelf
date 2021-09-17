<template>
  <base-card>
    <div class="heading">
      <h2>{{ info.title }}</h2>
      <a class="delete" href="#" @click="deleteCard">Delete</a>
    </div>
    <p>{{ info.description }}</p>
    <a class="link" :href="info.link">View Resource</a>
  </base-card>
</template>

<script>
import BaseCard from './basecomponents/BaseCard.vue'
export default {
  props: ['info'],
  components: {
    BaseCard
  },
  methods: {
    deleteCard() {
      this.$emit('delete-card', this.info.id)
    }
  }
}
</script>

<style scoped>
.heading {
  @apply flex justify-between items-center mb-5
}

.delete {
  @apply mr-8 text-lg font-semibold text-purple-600 hover:text-purple-800
}

h2 {
  @apply font-bold text-3xl
}

p {
  @apply text-xl mb-2
}

.link {
  @apply font-semibold text-xl text-red-600 hover:text-red-800
}
</style>