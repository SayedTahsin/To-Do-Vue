<script setup>
const props = defineProps(["allTask", "page"]);
const emit = defineEmits(["changingStatus"]);

const Doit = (event, id) => {
  emit("changingStatus", id, event.target.checked);
};
</script>

<template>
  <div v-if="props.page == 'All'">
    <div v-for="task in props.allTask" :class="{ taskClass: true, completed: task.status }">
      <label :for="task.id">{{ task.taskName }}</label>
      <input :id="task.id" :checked="task.status" type="checkbox" @change="Doit($event, task.id)" />
    </div>
  </div>

  <div v-else-if="props.page == 'Completed'">
    <div v-for="task in allTask">
      <div v-if="task.status === true" :class="{ taskClass: true, completed: task.status }">
        <label :for="task.id">{{ task.taskName }}</label>
        <input :id="task.id" :checked="task.status" type="checkbox" @change="Doit($event, task.id)" />
      </div>
    </div>
  </div>
  <div v-else>
    <div v-for="task in allTask">
      <div v-if="task.status === false" :class="{ taskClass: true, completed: task.status }">
        <label :for="task.id">{{ task.taskName }}</label>
        <input :id="task.id" :checked="task.status" type="checkbox" @change="Doit($event, task.id)" />
      </div>
    </div>
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
