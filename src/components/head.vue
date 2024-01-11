<script setup>
import { inject, ref } from "vue";

const allTask = inject("allTask");
const newTask = ref("");
const addTask = () => {
  if (newTask.value != "") {
    allTask.value.push({
      id: Date.now(),
      taskName: newTask.value,
    });
    newTask.value = "";
  }
};
</script>

<template>
  <div class="head">
    <h1>My To-Do List</h1>
    <input v-model="newTask" @keypress.enter="addTask" />
    <button @click="addTask">Add</button>
  </div>

  <br />
  <hr />
  <br />
</template>

<style scoped>
.head {
  text-align: center;
}

button {
  margin: 2px;
}
</style>
