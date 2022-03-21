<template>
  <h1 class="mt-20 mb-10 text-2xl font-semibold text-center text-emerald-600">My Projects</h1>
  <filter-nav @filterChange="current= $event" :current="current" />
  <div v-if="projects.length" class="text-center">
    <div v-for="project in filteredProjects" :key="project.id">
      <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete"/>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import SingleProject from '../components/SingleProject.vue'
import FilterNav from '../components/FilterNav.vue'

export default {
  name: 'Home',
  components: {
    SingleProject,
    FilterNav
  },
  data() {
    return{
      projects: [],
      // default filter will be 'all' to show all projects
      current: 'all'
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
  },
  computed: {
    filteredProjects() {
      if (this.current === 'completed') {
        return this.projects.filter(project => project.complete)
      }
      if (this.current === 'ongoing') {
        return this.projects.filter(project => !project.complete)
      }
      return this.projects
    }
  }

}
</script>
