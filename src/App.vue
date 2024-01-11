<script setup>
import { ref, computed, provide } from "vue";
import Task from "./components/task.vue";
import Head from "./components/head.vue";
import Foot from "./components/foot.vue";

const allTask = ref([]);
const completedTask = ref([]);
const pendingTask = computed(() => {
  return allTask.value.filter(
    (item1) => !completedTask.value.some((item2) => item1.id === item2.id)
  );
});
const page = ref("All");

provide("completedTask", completedTask);
provide("allTask", allTask);
provide("page", page);
</script>

<template>
  <div class="main">
    <Head />

    <div v-if="page === 'All'">
      <Task v-for="task in allTask" :taskname="task.taskName" :id="task.id" />
    </div>
    <div v-else-if="page === 'Completed'">
      <Task v-for="task in completedTask" :taskname="task.taskName" :id="task.id" />
    </div>
    <div v-else>
      <Task v-for="task in pendingTask" :taskname="task.taskName" :id="task.id" />
    </div>

    <Foot @changePage="(val) => (page = val)" />
  </div>
</template>

<style scoped>
.main {
  width: 400px;
  margin: auto;
  margin-top: 30px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  padding: 20px;
  border-radius: 10px;
}
</style>
