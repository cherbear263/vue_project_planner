<template>
<navbar class="fixed top-0 left-0 right-0"/>
<div class="max-w-full mx-4 mt-24 md:max-w-md md:mx-auto ">

  <router-view/>
  </div>
</template>
<script>
  import Navbar from './components/Navbar.vue'
export default {
  components: {
    Navbar
  }

}
</script>