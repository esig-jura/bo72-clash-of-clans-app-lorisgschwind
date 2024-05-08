<script setup>
// Definition des propritéts du composant

  defineProps({
  or: {
  type: Number,
  required: true
}
})
</script>


<template>

  <aside class="solde-or">
    <div>
      <img src="/img/piece-or-note.jpg" alt="Solde Or">
      {{ or.toLocaleString('fr-CH') }}
      pièces d'or
    </div>
    <div>
      <img src="/img/troupes-icon.png" alt="Troupes">
      0 troupes formées
    </div>
  </aside>

</template>

<style scoped>

</style>