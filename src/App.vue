<template>

<form action="" @submit.prevent="addTodo">

  <fieldset role="group">
  <input type="text" placeholder="Tâche a effectuer" v-model="newTodo">
  <button :disabled="newTodo.length ===0">Ajouter</button>
  </fieldset>

</form>
<div v-if="todos.length ===0">Vous n'avez pas de tache a faire :(</div>

<div v-else>
  <ul>
    <li v-for="todo in todos"
    :key="todo.date">
    {{ todo.title }}
  </li>
  </ul>
</div>

</template>

<script setup>
import { ref } from 'vue';


const newTodo = ref('')
const todos = ref ([])

// Fonction pour ajouter une tâche
const addTodo = () => {
  todos.value.push({
    title: newTodo.value,
    completed: false,
    date: Date.now()
  })
  newTodo.value =""
}

</script>

<style>
</style>