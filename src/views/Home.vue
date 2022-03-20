<template>
  <h1 class="mt-20 mb-10 text-center text-2xl text-emerald-600 font-semibold">My Projects</h1>
  <div v-if="projects.length" class="text-center">
    <div v-for="project in projects" :key="project.id">
      <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete"/>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import SingleProject from '../components/SingleProject.vue'

export default {
  name: 'Home',
  components: {
    SingleProject
  },
  data() {
    return{
      projects: []
    }
  },
  mounted() {
    fetch('http://localhost:3000/projects')
    .then(res => res.json())
    .then(data => this.projects = data)
    .catch(err => console.log(err.message))
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => {
        return project.id !== id
      })
    },
    handleComplete(id) {
      // find the project with the given id
      // toggle complete (locally)
      let p = this.projects.find(project => {
        return project.id === id
      })
      p.complete = !p.complete
    }
  }
}
</script>
