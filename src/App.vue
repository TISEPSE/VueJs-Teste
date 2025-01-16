<template>
  <form action="" @submit.prevent="addTodo">
    <fieldset role="group">
      <input type="text" placeholder="Tâche à effectuer" v-model="newTodo">
      <button :disabled="newTodo.length === 0">Ajouter</button>
    </fieldset>
  </form>
  
  <div v-if="todos.length === 0">Vous n'avez pas de tâche à faire :(</div>
  
  <div v-else>
    <ul>
      <li v-for="todo in sortedTodo()"
          :key="todo.date"
          :class="{completed: todo.completed}">
        <label>
          <input type="checkbox" v-model="todo.completed">about:blank#blocked
          {{ todo.title }}
        </label>
      </li>
    </ul>
    <label>
      <input type="checkbox" v-model="hideCompleted"> Masquer les tâches complétées
    </label>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const hideCompleted = ref(false);
const newTodo = ref('');
const todos = ref([
  {
    title: 'Aller promener le chien',
    completed: true,
    date: Date.now(),
  },
  {
    title: "Changer l'ampoule de la voiture",
    completed: false,
    date: Date.now(),
  },
]);

// Fonction pour ajouter une tâche
const addTodo = () => {
  todos.value.push({
    title: newTodo.value,
    completed: false,
    date: Date.now(),
  });
  newTodo.value = "";
};

// Fonction pour trier et filtrer les tâches
const sortedTodo = () => {
  const sortedTodos = todos.value.slice().sort((a, b) => a.completed > b.completed ? 1 : -1);
  if (hideCompleted.value) {
    return sortedTodos.filter(t => !t.completed);
  }
  return sortedTodos;
};
</script>

<style>
.completed {
  opacity: 50%;
  text-decoration: line-through;
}

ul {
  list-style-type: none;
  padding-left: 0;
}

li {
  margin: 0.5rem 0;
}
</style>
