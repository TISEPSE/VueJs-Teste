<template>

<form action="" @submit.prevent="addTodo">

  <fieldset role="group">
  <input type="text" placeholder="Tâche a effectuer" v-model="newTodo">
  <button :disabled="newTodo.length === 0">Ajouter</button>
  </fieldset>

</form>
<div v-if="todos.length === 0">Vous n'avez pas de tache a faire :(</div>

<div v-else>
  <ul>
    <li v-for="todo in sortedTodo()"
        :key="todo.date"
        :class="{completed: todo.completed}">
    <label>
      <input type="checkbox" v-model="todo.completed">
      {{ todo.title }}
    </label>
  </li>
  </ul>
</div>

</template>

<script setup>
import { ref } from 'vue';


const newTodo = ref('')
const todos = ref ([{
  title: 'Aller promener le chien',
  completed: true,
  date: Date.now(),
}, {
  title: "Changer l'ampoule de la voiture",
  completed: false,
  date: Date.now(),
}])

// Fonction pour ajouter une tâche
const addTodo = () => {
  todos.value.push({
    title: newTodo.value,
    completed: false,
    date: Date.now()
  })
  newTodo.value =""
}

const sortedTodo = () => {
  return todos.value.toSorted((a, b) =>a.completed > b.completed ? 1 : -1)
}
</script>

<style>

.completed{
  opacity: 50%;
  text-decoration: line-through;
}

</style>