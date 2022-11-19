<script setup>
import { ref, computed } from "vue";
const task = ref("");
const tasks = ref([]);
const hideCompleted = ref(false);
const computedTasks = computed(() =>
  hideCompleted.value ? tasks.value.filter((task) => !task.done) : tasks.value
);

let id = 0;
const addTodo = () => {
  tasks.value.push({ id: id++, task: task.value, done: false });
  task.value = "";
};
const removeTask = (id) => {
  tasks.value = tasks.value.filter((task) => task.id !== id);
};
</script>
<template>
  <form @submit.prevent="addTodo">
    <label for="task">Task</label>
    <input id="task" v-model="task" />
    <button>Add task</button>
  </form>
  <ul>
    <li v-for="task in computedTasks" :key="task.id">
      <input type="checkbox" v-model="task.done" />
      {{ task.task }}
      <button class="remove" @click="removeTask(task.id)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? "Show all" : "Hide completed" }}
  </button>
</template>
<style scoped>
.remove {
  background: red;
  border: none;
  color: white;
  border-radius: 5px;
  padding: 5px 10px;
}
</style>
