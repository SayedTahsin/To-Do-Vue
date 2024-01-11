<script setup>
import { inject } from "vue";
defineProps(["id", "taskname"]);

const completedTask = inject("completedTask");
const isActive = (targetId) => {
  return completedTask.value.some((item) => item.id === targetId);
};


</script>

<template>
  <div :class="{ taskClass: true, completed: isActive(id) }">
    <label :for="id">{{ taskname }}</label>
    <input
      type="checkbox"
      :id="id"
      :value="{ id: id, taskName: taskname }"
      v-model="completedTask"
    />
  </div>
</template>

<style>
.taskClass {
  font-size: larger;
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  padding: 2px;
  margin-bottom: 2px;
}
.taskClass input {
  margin-bottom: 8px;
}
.completed {
  background-color: rgba(232, 232, 232, 0.664);
  text-decoration: line-through;
}
</style>
