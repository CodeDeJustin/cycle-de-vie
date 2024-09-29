<template>
  <div id="app">
    <h1>Cycle de vie d'un composant Vue</h1>
    
    <!-- Bouton pour créer le composant -->
    <button v-if="!afficherComposant" @click="afficherComposant = true">Créer le composant</button>
    
    <!-- Affiche le composant si afficherComposant est vrai -->
    <CycleDeVie v-if="afficherComposant" @destroy="afficherComposant = false" />
    
    <!-- Bouton pour détruire le composant dans le composant enfant -->
  </div>
</template>

<script>
import CycleDeVie from './components/CycleDeVie.vue';

export default {
  data() {
    return {
      afficherComposant: false, // Le composant n'est pas affiché par défaut
    };
  },
  components: {
    CycleDeVie
  }
};
</script>