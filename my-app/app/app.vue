<template>
  <!-- De ConfettiButton wordt nu herkend door de import hieronder -->
  <ConfettiButton />
</template>

<script setup>
// HET BELANGRIJKSTE: Je moet het component hier importeren!
// Dit zorgt ervoor dat Vue (of Nuxt) weet waar ConfettiButton voor staat.
import ConfettiButton from './components/ConfettiButton.vue'; 
</script>

<style>
/* Optioneel: Stijl de root-container in App.vue
  We gebruiken hier een simpele stijl om er zeker van te zijn dat de ConfettiButton 
  (die min-height: 100vh heeft) correct wordt weergegeven.
*/
body {
  margin: 0;
  padding: 0;
}
</style>
