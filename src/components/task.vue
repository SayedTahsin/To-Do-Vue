<script setup>
import { computed } from "vue";

const props = defineProps(["allTask", "page"]);
const emit = defineEmits(["changingStatus"]);

const filteredTask = computed(() => {
  const res = props.allTask.filter((element) => {
    if (props.page === "All") {
      return element;
    } else if (props.page === "Completed") {
      if (element.status === true) return element;
    } else {
      if (element.status === false) return element;
    }
  });
  return res;
});

const Doit = (event, id) => {
  emit("changingStatus", id, event.target.checked);
};
</script>

<template>
  <div v-for="task in filteredTask" :class="{ taskClass: true, completed: task.status }" >
    <label :for="task.id">{{ task.taskName }}</label> 
    <input :id="task.id" :checked="task.status" type="checkbox" @change="Doit($event, task.id)" />
  </div>
</template>

<style scoped>
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
