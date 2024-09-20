<template>
  <form action="" @submit.prevent="addTodo">
    <fieldset role="group">
      <input 
        type="text" 
        placeholder="Tâche à effectuer"
        v-model="todo"
      >
      <button type="button">Ajouter</button>
    </fieldset>
    <p>{{ todo }}</p>
  </form>
  <div v-if="todos.length === 0">Vous n'avez pas de tâches à faire :(</div>
</template>


<script setup>
  import { ref } from 'vue'

  const todos = ref([])
  const todo = ref('')

  function addTodo() {
    console.log('Add ToDo');
    
  }
</script>

<style scoped>

</style>
