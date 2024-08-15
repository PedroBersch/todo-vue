<script setup>
import { ref } from "vue";

// Data references
const tasks = ref(["Task One", "Task Two", "Task Three",`POR FAVOR ME DE UM 10`]);
const newTask = ref("");
const input = ref("");

// Add a new task
const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
};

// Delete a task
const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

// Filter tasks based on the search input
const filteredTasks = () => {
  return tasks.value.filter((taskName) =>
    taskName.toLowerCase().includes(input.value.toLowerCase())
  );
};
</script>

<template>
  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>
  <br />

  <h3>Task List:</h3>
  <br />
  <input type="text" v-model="input" placeholder="Search task..." />
  <br />
  <ul>
    <li v-for="(task, index) in filteredTasks()" :key="index">
      <span>{{ task }}</span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>
  <br />
</template>
