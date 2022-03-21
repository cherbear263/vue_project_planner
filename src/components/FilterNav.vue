<template>
  <nav class="filter-nav">
    <button class="mx-3 text-xs font-bold tracking-wide text-gray-400 uppercase border-0 outline-none cursor-pointer bg-none "
      @click="updateFilter('all')"
      :class="{ active: current === 'all'}"
      >View All</button>
    <button class="mx-3 text-xs font-bold tracking-wide text-gray-400 uppercase border-0 outline-none cursor-pointer bg-none "
      @click="updateFilter('completed')"
      :class="{ active: current === 'completed'}"
      >Completed</button>
    <button class="mx-3 text-xs font-bold tracking-wide text-gray-400 uppercase border-0 outline-none cursor-pointer bg-none "
      @click="updateFilter('ongoing')"
      :class="{ active: current === 'ongoing'}"
      >Ongoing</button>
    
  </nav>
</template>
<script>
export default {
  props: ['current'],
  methods: {
    updateFilter(by) {
      this.$emit('filterChange', by) 

    }
  }
}
</script>
<style>
.filter-nav button.active {
  color: #555;
}
</style>
