<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  titre: {
    type: String,
    required: true
  },
  description: {
    type: String,
    required: true

  }
});
</script>

<template>
  <header>
    <h1>
      <img src="/img/clash-of-clans-logo.webp" alt="Logo Clash of Clans">
      {{ titre }}
    </h1>
    <p class="description">
      {{ description }}
    </p>
  </header>
</template>

<style scoped lang="sass">
header
  padding: 80px 0 20px
  text-align: center

header h1 img
  max-height: 150px


header h1,
header .description
  font-size: 3.25rem
  color: white
  text-shadow: 1px 1px 2px black /* offset-x | offset-y | blur-radius | color */


header  h1
  margin: 0


header .description
  font-size: 1.5rem
  line-height: 1.25
  max-width: 640px
  margin: 0 auto 1em

</style>
