<template>
  <div class="container px-4 py-3 mx-auto my-3 text-left bg-white border-l-4 rounded-md shadow border-pink-600/50"
  :class="{complete: project.complete}">
    <div class="flex justify-between actions">
      <h3 class="text-lg font-semibold cursor-pointer"
      @click="showDetails = !showDetails">{{ project.title }}</h3>
    <div class="icons">
      <router-link :to="{ name: 'EditProject', params: { id: project.id }}">
        <span class="ml-2 text-lg text-gray-400 cursor-pointer material-icons hover:text-blue-600">edit</span></router-link>
      
      <span @click="deleteProject" class="ml-2 text-lg text-gray-400 cursor-pointer material-icons hover:text-pink-600">delete</span>
      <span @click="toggleComplete" class="ml-2 text-lg text-gray-400 cursor-pointer material-icons hover:text-emerald-600 tick">done</span>
    </div>

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
      showDetails: false,
      uri: 'http://localhost:3000/projects/' + this.project.id
    }
  },
  methods: {
    deleteProject() {
      fetch(this.uri, { method: 'DELETE'})
      .then(() => this.$emit('delete', this.project.id))
      .catch(err => console.log(err.message))

    },
    toggleComplete() {
      fetch(this.uri, { 
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ complete: !this.project.complete })
        }).then(() => this.$emit('complete', this.project.id))
        .catch(err => console.log(err))
    }
  }
}
</script>