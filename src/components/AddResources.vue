<template>
  <base-card>
    <form action="" @submit.prevent>
      <div class="form-section">
        <label for="Title">Title</label>
        <input class="form-inputs" type="text" name="Title" ref="title">
      </div>
      <div class="form-section">
        <label for="Description">Description</label>
        <textarea class="form-inputs" name="Description" rows="3" ref="description"></textarea>
      </div>
      <div class="form-section">
        <label for="Link">Link</label>
        <input class="form-inputs" type="text" name="Link" ref="link">
      </div>
      <div>
        <button class="submit" @click="addResource">Add Resource</button>
      </div>
    </form>
  </base-card>
  <teleport to="#app">
    <div class="invalid-background" v-if="invalidAlert">
      <div class="invalid-card">
        <div class="invalid-header">
          <h2>Invalid Input</h2>
        </div>
        <div class="invalid-content">
          <div class="invalid-message">
            <p>Unfortunately, at least one input value is invalid.</p>
            <p>Please check all inputs and make sure you enter at least a few characters into each input field</p>
          </div>
          <div class="invalid-footer">
            <button class="submit" @click="invalidAlert = false">Okay</button>
          </div>
        </div>
      </div>
    </div>
  </teleport>
</template>

<script>
import BaseCard from './basecomponents/BaseCard.vue'
export default {
  components: {
    BaseCard
  },
  data() {
    return {
      invalidAlert: false
    }
  },
  methods: {
    addResource() {
      if (!this.isValid()) {
        this.invalidAlert = true
      } else {
        this.$emit('new-resource', {
          id: Date.now(),
          title: this.$refs.title.value,
          description: this.$refs.description.value,
          link: this.$refs.link.value
        })
        this.resetInputs()
      }
    },
    isValid() {
      for (var ref in this.$refs) {
        if (this.$refs[ref].value.length < 1) {
          return false
        }
      }
      return true
    },
    resetInputs() {
      for (var ref in this.$refs) {
        this.$refs[ref].value = ""
      }
    }
  }
}
</script>

<style scoped>
form {
  @apply flex flex-col 
}

label {
  @apply font-semibold text-xl block mb-1
}

.form-inputs {
  @apply border-2 w-full text-lg focus:bg-purple-100 focus:outline-none focus:ring-2 focus:ring-purple-900
}

.form-section {
  @apply my-3
}

.submit {
  @apply text-lg py-4 px-10 mt-4 rounded-md text-white bg-purple-800 hover:bg-purple-900
}

.invalid-background {
  @apply bg-black bg-opacity-50 h-screen w-screen flex justify-center items-center fixed top-0
}

.invalid-card {
  @apply bg-white w-2/3 h-80 rounded-xl flex flex-col 
}

.invalid-header {
  @apply bg-purple-800 text-white font-bold text-3xl p-5 rounded-t-xl mb-4
}

.invalid-content {
  @apply p-5 text-lg flex-1 flex flex-col justify-between
}

p {
  @apply mb-2
}

.invalid-footer {
  @apply flex justify-end
}
</style>