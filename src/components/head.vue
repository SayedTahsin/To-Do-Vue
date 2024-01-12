<script setup>
import { ref } from "vue";

const newTask = ref("");
const emit = defineEmits(['addTask'])

const addTask = () => {
  if (newTask.value != "") {
    const taskObject = {id: Date.now(), taskName: newTask.value, status: false};
    emit('addTask',taskObject);
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
