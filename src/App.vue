<script setup>
// Cheat Sheet: https://steve-fallet.notion.site/Vue-3-script-setup-Cheat-Sheet-b12192ceae244ecda65f771579ca02bc
import {ref, onMounted} from 'vue'
import PageTopBarre from "@/components/PageTopBarre.vue";
import PageFooter from "@/components/PageFooter.vue";
import PageHeader from "@/components/PageHeader.vue";
import TroupeCarte from "@/components/TroupeCarte.vue";

// Tableau des troupes
const troupes = ref([])
const titre = 'Clash of Clans';
const description = 'Construire un village, former un clan et participer à des guerres de clans épiques !';
// Pièces d'or
let totalOr = ref(100000);

//Tableau des troupes formées
let nbTroupesFormées = ref(0);

// Quand le composant est monté, on va chercher les données
onMounted(() => {
  fetch('https://cocapi.divtec.me/troupes') //Appel à l'API
      .then((res) => res.json()) //On recupere les donnes en json
      .then((data) => { // On recupere les données en format javascript
        troupes.value = data //On les stock dans la variables troupe
      })
})

/* Méthodes */
function formerTroupe(troupe) {
  if (totalOr.value < troupe.cout) {
    alert("Vous n'avez pas assez d'or mon seigneur !")
    return
  }
  totalOr.value -= troupe.cout
  nbTroupesFormées.value +=1;
}
</script>

<template>
  <RouterView />

<PageTopBarre :or = "totalOr" :troupesFormees="nbTroupesFormées"/>

  <PageHeader :titre="titre" :description="description" />
  <main>
    <ul class="cartes">
      <li v-for="trp in troupes" :key="trp.id">
        <troupe-carte :troupe="trp" :or="totalOr" @former="formerTroupe"/>
      </li>
    </ul>
  </main>
<PageFooter />
</template>

<style scoped lang="sass">

</style>