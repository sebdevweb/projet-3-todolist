<template>
  <form @submit.prevent="addTodo">
    <fieldset role="group">
      <input 
        type="text" 
        placeholder="Tâche à effectuer"
        v-model="newTodo"
      >
      <button :disabled="newTodo.length == 0">Ajouter</button>
    </fieldset>
  </form>
  <div v-if="todos.length == 0">Vous n'avez pas de tâches à faire :(</div>
  <div v-else>
    <ul>
      <li 
        v-for="todo in todos"
        :key="todo.date"
      >
      <label>
        <input type="checkbox">
        {{ todo.title }}
      </label>
      </li>
    </ul>
  </div>
</template>


<script setup>
  import { ref } from 'vue'

  const newTodo = ref('')
  const todos = ref([])

  const addTodo = () => {
    todos.value.push({
      title: newTodo.value,
      completed: false,
      date: Date.now()
    })
    console.log(newTodo.value);
    newTodo.value = ''
    
  }
</script>

<style scoped>

</style>
