<template>
  <div class="text-left container my-3 mx-auto bg-white py-2 px-4 rounded-md shadow border-l-8 border-pink-600/50">
    <div class="actions">
      <h3 class="text-lg font-semibold cursor-pointer"
      @click="showDetails = !showDetails">{{ project.title }}</h3>

    </div>
  <div v-if="showDetails">
    <p>{{ project.details }}</p>
  </div>
  </div>
</template>
<script>
export default {
  name: 'SingleProject',
  props: ['project'],
  data() {
    return {
      showDetails: false
    }
  }
}
</script>