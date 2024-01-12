<script setup>
const props = defineProps(['page'])
</script>

<template>
  <div class="filterButton">
    <button @click="$emit('changePage', 'All')" :class="{ active: props.page === 'All' }" > All Task </button>
    <button @click="$emit('changePage', 'Completed')" :class="{ active: props.page === 'Completed' }" > Completed Task </button>
    <button @click="$emit('changePage', 'Pending')" :class="{ active: props.page === 'Pending' }" > Pending Task </button>
  </div>
</template>

<style scoped>
.filterButton {
  text-align: center;
}
button {
  margin: 2px;
}
.active {
  font-weight: bold;
}
</style>
