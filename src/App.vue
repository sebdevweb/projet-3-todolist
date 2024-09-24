<template>
  <button @click="showTimer = !showTimer">Show/Hide</button>
  <Timer v-if="showTimer == true" />
  <Layout>
    <template #aside>
      Contenu Aside
    </template>
    <template v-slot:main>
      Contenu Main
    </template>
    <template v-slot:footer>
      Contenu Footer
    </template>
    
  </Layout>
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
        v-for="todo in sortedTodos"
        :key="todo.date"
        :class="{completed: todo.completed}"
      >
      <Checkbox :label="todo.title" 
        
      />
      </li>
    </ul>
    <label><input type="checkbox" v-model="hideCompleted">Masquer les tâches effectuées.</label>
    <p v-if="remainingTodos > 0">{{ remainingTodos }} tâche{{ remainingTodos > 1 ? 's' : ''}} à restante{{remainingTodos > 1 ? 's' : ''}}</p>
    <Checkbox :label="'Bonjour'"/>
  </div>
</template>


<script setup>
  import { computed, onMounted, ref } from 'vue';
  import Checkbox from './Checkbox.vue';
  import Button from './Button.vue';
  import Layout from './Layout.vue';
  import Timer from './Timer.vue';

  const newTodo = ref('')
  const todos = ref([])

  onMounted(() => {
    fetch('https://jsonplaceholder.typicode.com/todos') // Récupère les données depuis ce serveur
    .then(recup => recup.json()) // Récupère le json
    .then(v => todos.value = v) // Liste de tâches à récupérer dans une variable 'v' et changer la valeur de la ref pour pouvoir récupérer les données depuis le serveur
    
  })
  const hideCompleted = ref(false)

  const showTimer = ref(true)

  const addTodo = () => {
    todos.value.push({
      title: newTodo.value,
      completed: false,
      date: Date.now()
    })
    console.log(newTodo.value);
    newTodo.value = ''
  }

  const sortedTodos = computed(() => {
    console.log('demo');
    
    const sortedTodos =  todos.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1)
    if(hideCompleted.value == true) {
      return sortedTodos.filter(t => t.completed == false)
    }
    return sortedTodos
  })

  const remainingTodos = computed(() => {
    return todos.value.filter(t => t.completed == false).length
  })
  
</script>

<style scoped>
  .completed {
    opacity: .5;
    text-decoration: line-through;
  }
</style>
