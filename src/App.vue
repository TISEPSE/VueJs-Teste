<template>
  <h1 v-show="tasks.length === 0" class="style">Vous n'avez pas de tâche en cours</h1>
  <form action="" @submit.prevent="addTask">
    <input type="text" placeholder="ex: Achetez du pain" v-model="taskValue">
    <button>Ajouter</button>
  </form>
  <br>
  <hr>
  <ul>
    <li v-for="(task, index) in tasks" :key="index">
      {{ task }} <button @click="removeTask(task)">Supprimer</button>
    </li>
  </ul>
</template>

<script setup>
import { ref } from "vue";

// Liste des tâches
const tasks = ref([]);

// Valeur de la nouvelle tâche
const taskValue = ref("");

// Ajouter une tâche
const addTask = () => {
  tasks.value.push(taskValue.value);
  taskValue.value = "";
};

// Supprimer une tâche
const removeTask = (task) => {
  tasks.value = tasks.value.filter(m => m !== task);
};
</script>

<style>
.style {
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}

button {
  margin: 0 5px;
}
</style>