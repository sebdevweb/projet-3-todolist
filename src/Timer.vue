<template>
  <div ref="div">
    Temps : {{ time }} <br />
    Largeur : {{ size.width }}, Hauteur : {{ size.height }}
  </div>
</template>

<script setup>
  import { onMounted, onUnmounted, ref } from 'vue'

  const div = ref(null)
  const time = ref(0)
  let timer = ref(0)
  const size = ref({
    width: 0,
    height: 0
  })

  onMounted(() => {
    const rect = div.value.getBoundingClientRect()
    size.value = { width: rect.width, height: rect.height }
    
    timer = setInterval(() => {
      console.log('increment'); // Ce log permet de voir que la fonction du composant s'incrémente toujours (effet de bord)
      
      time.value++
    }, 1000)
  })

  onUnmounted(() => {
    clearInterval(timer) // Permet de supprimer l'effet de bord laissé par l'incrémentation et optimise les performances de l'app.
  })
</script>