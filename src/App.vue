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
        v-for="todo in sortedTodos"
        :key="todo.date"
        :class="{completed: todo.completed}"
      >
      <Checkbox :label="todo.title" 
        @check="(p) => console.log('coché', p)" 
        @uncheck="console.log('décoché')" 
      />
      </li>
    </ul>
    <label><input type="checkbox" v-model="hideCompleted">Masquer les tâches effectuées.</label>
    <p v-if="remainingTodos > 0">{{ remainingTodos }} tâche{{ remainingTodos > 1 ? 's' : ''}} à restante{{remainingTodos > 1 ? 's' : ''}}</p>
    <Checkbox :label="'Bonjour'"/>
  </div>
</template>


<script setup>
  import { computed, ref } from 'vue'
  import Checkbox from './Checkbox.vue';

  const newTodo = ref('')
  const todos = ref([{
      title: 'Taches effectué',
      completed: true,
      date: 1
    }, {
      title: 'Taches à faire',
      completed: false,
      date: 2
    },
  ])
  const hideCompleted = ref(false)

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
