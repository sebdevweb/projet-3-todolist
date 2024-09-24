<template>
  <input type="text" v-model="name" placeholder="Changer le titre de la page">
</template>

<script setup>
  import { ref, watch } from 'vue'

  const name = ref('')

  watch(name, (newValue) => {
    document.title = newValue
  })
</script>