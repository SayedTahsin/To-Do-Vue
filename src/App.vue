<script setup>
import { ref } from "vue";
import Task from "./components/task.vue";
import Head from "./components/head.vue";
import Foot from "./components/foot.vue";

const allTask = ref([]);
const page = ref("All");

const changeStatus = (id, checked) => {
  const index = allTask.value.findIndex((obj) => obj.id === id);
  allTask.value[index].status = checked;
};
</script>

<template>
  <div class="main">
    <Head @addTask="(val) => { allTask.push(val); }" />
    <Task :allTask="allTask" :page="page" @changingStatus="changeStatus" />
    <Foot :page="page" @changePage="(val) => (page = val)" />
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
