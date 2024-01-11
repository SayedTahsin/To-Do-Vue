<script setup>
import { ref, computed } from "vue";

const newTask = ref("");
const allTask = ref([]);
const completedTask = ref([]);
const pendingTask = computed(() => {
  return allTask.value.filter(
    (item1) => !completedTask.value.some((item2) => item1.id === item2.id)
  );
});
const page = ref(1);

const addTask = () => {
  allTask.value.push({
    id: Date.now(),
    taskName: newTask.value,
  });
  newTask.value = "";
};
</script>

<template>
  <div class="main">
    <div class="head">
      <h1>My To-Do List</h1>
      <input v-model="newTask" @keypress.enter="addTask" />
      <button @click="addTask">Add</button>
    </div>

    <br />
    <br />
    <hr />
    <br />

    <div v-if="page == 1">
      <div v-for="task in allTask" class="task">
        <label for="{{task.id}}">{{ task.taskName }}</label>
        <input
          id="{{task.id}}"
          type="checkbox"
          :value="{ id: task.id, taskName: task.taskName }"
          v-model="completedTask"
        />
      </div>
    </div>

    <div v-else-if="page == 2">
      <div v-for="task in completedTask" class="task">
        <label for="{{task.id}}">{{ task.taskName }}</label>
        <input
          id="{{task.id}}"
          type="checkbox"
          :value="{ id: task.id, taskName: task.taskName }"
          v-model="completedTask"
        />
      </div>
    </div>

    <div v-else>
      <div v-for="task in pendingTask" class="task">
        <label for="{{task.id}}">{{ task.taskName }}</label>
        <input
          id="{{task.id}}"
          type="checkbox"
          :value="{ id: task.id, taskName: task.taskName }"
          v-model="completedTask"
        />
      </div>
    </div>

    <div class="filterButton">
      <button @click="page = 1">All Task</button>
      <button @click="page = 2">Completed Task</button>
      <button @click="page = 3">Pending Task</button>
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
.task {
  font-size: larger;
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
}
</style>
