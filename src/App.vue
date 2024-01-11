<script setup>
import { ref, computed, provide } from "vue";
import Task from "./components/task.vue";

const newTask = ref("");
const allTask = ref([]);
const completedTask = ref([]);
const pendingTask = computed(() => {
  return allTask.value.filter(
    (item1) => !completedTask.value.some((item2) => item1.id === item2.id)
  );
});

const page = ref("All");

const addTask = () => {
  if (newTask.value != "") {
    allTask.value.push({
      id: Date.now(),
      taskName: newTask.value,
    });
    newTask.value = "";
  }
};

provide("completedTask", completedTask);
</script>

<template>
  <div class="main">
    <div class="head">
      <h1>My To-Do List</h1>
      <input v-model="newTask" @keypress.enter="addTask" />
      <button @click="addTask">Add</button>
    </div>

    <br />
    <hr />
    <br />

    <div v-if="page === 'All'">
      <Task v-for="task in allTask" :taskname="task.taskName" :id="task.id" />
    </div>
    <div v-else-if="page === 'Completed'">
      <Task v-for="task in completedTask" :taskname="task.taskName" :id="task.id" />
    </div>
    <div v-else>
      <Task v-for="task in pendingTask" :taskname="task.taskName" :id="task.id"
      />
    </div>

    <div class="filterButton">
      <button @click="page = 'All'" :class="{ active: page == 'All' }"> All Task </button>
      <button @click="page = 'Completed'" :class="{ active: page == 'Completed' }" > Completed Task </button>
      <button @click="page = 'Pending'" :class="{ active: page == 'Pending' }"> Pending Task </button>
    </div>
  </div>
</template>


<style>
.main {
  width: 400px;
  margin: auto;
  margin-top: 30px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  padding: 20px;
  border-radius: 10px;
}
.head,
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
