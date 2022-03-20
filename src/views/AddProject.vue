<template>
  <h1 class="my-10 text-center text-2xl text-emerald-600 font-semibold">Add a project</h1>
  <form @submit.prevent="handleSubmit" class="bg-white p-4 rounded-sm my-8">
    <label class="block uppercase text-sm font-bold tracking-tight my-2 mx-2 text-gray-500">Title:</label>
    <input type="text" v-model="title" required class="p-4 border-b-2 border-b-gray-200 w-full focus:outline-emerald-500 mb-4"/>
    <label class="block uppercase text-sm font-bold tracking-tight my-2 mx-2 text-gray-500">Details: </label>
    <textarea v-model="details" required class="border-2 border-gray-200 p-4 w-full h-80 focus:outline-emerald-500"></textarea>
    <button type="submit" class="block mt-3 mx-auto bg-emerald-500 p-4 border-0 rounded-sm text-sm text-white font-semibold uppercase">Add Project</button>
  </form>
</template>
<script>
export default {
  data() {
    return {
      title: '',
      details: ''
    }
  },
  methods: {
    handleSubmit() {
      let project = {
        title: this.title,
        details: this.details,
        complete: false
      }
      fetch('http://localhost:3000/projects', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(project)
      }).then(() => {
        // once post added redirect to home page
        this.$router.push('/')
      }).catch((err) => console.log(err))
    }
  }
}
</script>