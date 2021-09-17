<template>
  <the-header></the-header>
  <main class="container mx-auto mt-10">
    <navigation :active-tab="activeTab" @change-tab="switchTab"></navigation>
    <keep-alive>
      <component 
      :is="activeElement" 
      :resources="resources" 
      @delete-resource="deleteResource"
      @new-resource="addResource"></component>
    </keep-alive>
  </main>
</template>

<script>
import TheHeader from './components/singlecomponents/TheHeader.vue'
import Navigation from './components/Navigation.vue'
import ViewResources from './components/ViewResources.vue'
import AddResources from './components/AddResources.vue'

export default {
  components: {
    TheHeader,
    Navigation,
    ViewResources,
    AddResources
  },
  data() {
    return {
      activeTab: 'stored',
      resources: [
        {
          id: 0,
          title: 'Google',
          description: 'You need to know how to google!',
          link: 'https://www.google.com/'
        },
        {
          id: 1,
          title: 'Official Guide',
          description: 'The official Vue.js documentation',
          link: 'https://v3.vuejs.org/'
        }
      ]
    }
  },
  computed: {
    activeElement() {
      switch(this.activeTab) {
        case 'stored':
          return 'view-resources';
        case 'add':
          return 'add-resources';
      }
    }
  },
  methods: {
    switchTab(id) {
      this.activeTab = id
    },
    deleteResource(id) {
      this.resources = this.resources.filter(item => item.id !== id)
    },
    addResource(newResource) {
      this.resources.push(newResource)
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap');

html {
  font-family: 'Poppins', sans-serif;
}
</style>
