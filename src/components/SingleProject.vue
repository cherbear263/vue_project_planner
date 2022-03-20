<template>
  <div class="text-left container my-3 mx-auto bg-white py-3 px-4 rounded-md shadow border-l-4 border-pink-600/50"
  :class="{complete: project.complete}">
    <div class="actions flex justify-between">
      <h3 class="text-lg font-semibold cursor-pointer"
      @click="showDetails = !showDetails">{{ project.title }}</h3>
    <div class="icons">
      <span class="material-icons text-lg cursor-pointer text-gray-400 ml-2 hover:text-blue-600">edit</span>
      <span @click="deleteProject" class="material-icons text-lg cursor-pointer text-gray-400 ml-2 hover:text-pink-600">delete</span>
      <span @click="toggleComplete" class="material-icons text-lg cursor-pointer text-gray-400 ml-2 hover:text-emerald-600 tick">done</span>
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