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
      <li v-for="todo in sortedTodo" :key="todo.date" :class="{ completed: todo.completed }">
        <Checkbox :label="todo.title" @check="console.log('coché')" @unchecked="console.log('décocher')" />
      </li>
    </ul>

    <label>
      <input type="checkbox" v-model="hideCompleted"> Masquer les tâches complétées
    </label>

    <p v-if="remainingTodo > 0">
      {{ remainingTodo }} tâche{{ remainingTodo > 1 ? "s" : "" }} à faire
    </p>

    <Checkbox label="Bonjour"/>

  </div>
</template>

<script setup>
import { computed, ref } from 'vue';
import Checkbox from './Checkbox.vue'; 

const hideCompleted = ref(false); 
const newTodo = ref('');
const todos = ref([
  {
    title: 'Aller promener le chien',
    completed: true,
    date: Date.now()
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
const sortedTodo = computed(() => {
  const sortedTodos = todos.value.slice().sort((a, b) => a.completed > b.completed ? 1 : -1);
  if (hideCompleted.value) {
    return sortedTodos.filter(t => !t.completed);
  }
  return sortedTodos;
});

const remainingTodo = computed(() => {
  return todos.value.filter(t => t.completed === false).length;
});
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
