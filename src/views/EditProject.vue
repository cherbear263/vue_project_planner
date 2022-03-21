<template>
  <h1 class="my-10 text-2xl font-semibold text-center text-emerald-600">Edit project</h1>
  <form @submit.prevent="handleSubmit" class="p-4 my-8 bg-white rounded-sm">
    <label class="block mx-2 my-2 text-sm font-bold tracking-tight text-gray-500 uppercase">Title:</label>
    <input type="text" v-model="title" required class="w-full p-4 mb-4 border-b-2 border-b-gray-200 focus:outline-emerald-500"/>
    <label class="block mx-2 my-2 text-sm font-bold tracking-tight text-gray-500 uppercase">Details: </label>
    <textarea v-model="details" required class="w-full p-4 border-2 border-gray-200 h-80 focus:outline-emerald-500"></textarea>
    <button type="submit" class="block p-4 mx-auto mt-3 text-sm font-semibold text-white uppercase border-0 rounded-sm bg-emerald-500">Update Project</button>
  </form>
</template>

<script>
export default {
  props: ['id'],
  data() {
    return {
      title: '',
      details: '',
      uri: 'http://localhost:3000/projects/' + this.id
    }
  },
  mounted() {
    fetch(this.uri)
      .then(res => res.json())
      .then(data => {
        this.title = data.title
        this.details = data.details
      })
  },
  methods: {
    handleSubmit() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({title: this.title, details: this.details})
      }).then(() => {
        // once post added redirect to home page
        this.$router.push('/')
      }).catch((err) => console.log(err))
    }
  
  }
  
}
</script>