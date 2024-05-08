<script setup>
// Cheat Sheet: https://steve-fallet.notion.site/Vue-3-script-setup-Cheat-Sheet-b12192ceae244ecda65f771579ca02bc
import {ref, onMounted} from 'vue'
import PageTopBarre from "@/components/PageTopBarre.vue";
import PageFooter from "@/components/PageFooter.vue";
import PageHeader from "@/components/PageHeader.vue";

// Tableau des troupes
const troupes = ref([])

// Pièces d'or
let totalOr = ref(100000);

// Quand le composant est monté, on va chercher les données
onMounted(() => {
  fetch('https://cocapi.divtec.me/troupes') //Appel à l'API
      .then((res) => res.json()) //On recupere les donnes en json
      .then((data) => { // On recupere les données en format javascript
        troupes.value = data //On les stock dans la variables troupe
      })
})
</script>

<template>
<PageTopBarre :or = "totalOr" />

  <PageHeader />
  <main>
    <ul class="cartes">
      <li v-for="troupe in troupes" :key="troupe.id">
        <article>
          <header :style="'background: linear-gradient(60deg,#3B3B3B 0%, ' + troupe.couleur + ' 100%);'">
            <img :src="troupe.image"
                 :alt="troupe.nom">
          </header>
          <div class="level" :style="'color:'+ troupe.couleur+ ' ;'">
           Niveau {{ troupe.niveau }}
          </div>
          <h2 class="name">{{troupe.nom}}</h2>
          <button :style="'background-color: ' + troupe.couleur +';'"> Former
            <img src="/img/piece-or.png" alt="Former"></button>
          <p class="description">{{troupe.description}}</p>
          <footer>
            <div class="training"
                 :style="'background-color: ' + troupe.couleur +';'">
              <div>{{ troupe.formation }}<sup>sec</sup></div>
              <div>Formation</div>
            </div>
            <div class="speed"
                 :style="'background-color: ' + troupe.couleur +';'">
              <div>{{ troupe.vitesse }}</div>
              <div>Vitesse</div>
            </div>
            <div class="cost"
                 :style="'background-color: ' + troupe.couleur +';'">
              <div>{{ troupe.cout }}</div>
              <div>Coût</div>
            </div>
          </footer>
        </article>
      </li>
    </ul>
  </main>
<PageFooter />
</template>

<style scoped lang="sass">

</style>