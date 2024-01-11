<script setup>
import { inject, ref } from "vue";
const page = inject("page");
</script>

<template>
  <div class="filterButton">
    <button
      @click="$emit('changePage', 'All')"
      :class="{ active: page == 'All' }"
    >
      All Task
    </button>
    <button
      @click="$emit('changePage', 'Completed')"
      :class="{ active: page == 'Completed' }"
    >
      Completed Task
    </button>
    <button
      @click="$emit('changePage', 'Pending')"
      :class="{ active: page == 'Pending' }"
    >
      Pending Task
    </button>
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
