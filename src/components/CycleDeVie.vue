<template>
  <div>
    <h1>{{ message }}</h1>
    <p>Compteur : {{ compteur }}</p>
    <p>Étape actuelle du cycle de vie : {{ etapeCycleDeVie }}</p>

    <!-- Bouton pour mettre à jour le compteur -->
    <button @click="mettreAJourCompteur">Mettre à jour le compteur</button>
    
    <!-- Bouton pour détruire le composant -->
    <button @click="detruireComposant">Détruire le composant</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: "Bienvenue dans le cycle de vie Vue.js !",
      compteur: 0,
      intervalId: null,
      etapeCycleDeVie: "Aucune étape pour l'instant", // Affiche l'étape actuelle
    };
  },

  created() {
    this.etapeCycleDeVie = "Le composant a été créé (created)";
  },

  beforeMount() {
    this.etapeCycleDeVie = "Le DOM virtuel est prêt (beforeMount)";
  },

  mounted() {
    this.etapeCycleDeVie = "Le composant est monté dans le DOM (mounted)";
    this.intervalId = setInterval(() => {
      this.compteur++;
    }, 1000);
  },

  beforeUpdate() {
    // Ne pas afficher le log à chaque mise à jour réactive du compteur pour éviter les boucles infinies
    if (this.compteur % 10 === 0) { // Par exemple, seulement quand le compteur est divisible par 10
      console.log("Le DOM va être mis à jour (beforeUpdate)");
    }
  },

  updated() {
    // Pareil ici, afficher seulement dans certaines conditions
    if (this.compteur % 10 === 0) {
      console.log("Le DOM a été mis à jour (updated)");
    }
  },

  beforeUnmount() {
    this.etapeCycleDeVie = "Le composant va être retiré du DOM (beforeUnmount)";
    clearInterval(this.intervalId);
  },

  unmounted() {
    console.log("Le composant a été détruit (unmounted)");
  },

  methods: {
    mettreAJourCompteur() {
      this.compteur++;
      this.etapeCycleDeVie = "Mise à jour du compteur manuellement";
    },

    detruireComposant() {
      this.$emit("destroy");
    }
  }
};
</script>

<style scoped>
h1 {
  color: #42b983;
}
</style>