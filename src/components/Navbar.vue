<template>
  <nav class="h-16 mx-auto my-4 mt-0 text-center bg-emerald-500">
    <router-link class="inline-block pt-4 mx-3 text-lg text-gray-200" :to="{ name: 'Home' }">Projects</router-link>
    <router-link class="inline-block pt-4 mx-3 text-lg text-gray-200" :to="{ name: 'AddProject' }">Add a New Project</router-link>
  </nav>
</template>

<script>
export default {
  
}
</script>
<style scoped>
  a.router-link-active {
    border-bottom: 2px solid #fff;
    padding-bottom: 4px;
  }
</style>