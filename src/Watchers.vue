<template>
  <input type="text" v-model="page.title" placeholder="Changer le titre de la page">
  Temps écoulé : {{ time }}
  <button @click="reset">RESET</button>
</template>

<script setup>
  import { ref, watch, watchEffect } from 'vue'
import { useTimer } from './composable/useTimer';

  const {time, reset} = useTimer()

  const page = ref({
    title: ''
  })

  // fonction utile lorsque des effets de bord sortent du cadre de vue.js
  // sinon : fonction computed : lorsque besoin de dériver une valeur à partir d'une autre valeur réactive
  watchEffect(() => {
    document.title = page.value.title
  })
</script>