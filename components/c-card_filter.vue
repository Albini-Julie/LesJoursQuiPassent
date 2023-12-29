<template>
  <div class="e-card"></div>
  <div class="e-card__content">
    <div class="e-card__icons">
      <fleur_pointue v-if="fleur == 'pointue'" :couleur="couleur2" />
      <fleur_ronde v-else-if="fleur == 'ronde'" :couleur="couleur2" />
      <fleur_semieronde v-else-if="fleur == 'semieronde'" :couleur="couleur2" />
      <fleur_semieronde2
        v-else-if="fleur == 'semieronde2'"
        :couleur="couleur2"
      />
      <croix @click="inverserCardOpen" :couleur="couleur2" />
    </div>
    <div class="e-card__script">
      <h3 class="e-card__title">{{ title }}</h3>
      <p class="e-card__text">{{ text }}</p>
    </div>
  </div>
  <div class="e-card__button">
    <c-bouton
      size="small"
      variant="rounded"
      :couleur="couleur2"
      @click="toggleBool(filterChoice, 'true')"
      >Ajouter/Supprimer cette catégorie</c-bouton
    >
  </div>
</template>

<script setup>
import { card_open } from "@/config.js";
import { nazaBool, storyBool, cinemaBool, musicBool } from "@/config.js";

defineProps({
  couleur: String,
  couleur2: String,
  fleur: String,
  title: String,
  text: String,
  filterChoice: String,
});

// Ajoutez une méthode pour inverser la valeur de Card_open
const inverserCardOpen = () => {
  card_open.value = !card_open.value;
  console.log("Card_open", card_open.value);
};

const toggleBool = (theme, test) => {
  switch (theme) {
    case "naza":
      console.log("NazaBool :", nazaBool.value);
      nazaBool.value = !nazaBool.value;
      if (test == "true") {
        card_open.value = !card_open.value;
      }
      console.log("NazaBool :", nazaBool.value);
      return nazaBool.value;
    case "story":
      console.log("StoryBool :", storyBool.value);
      storyBool.value = !storyBool.value;
      if (test == "true") {
        card_open.value = !card_open.value;
      }
      console.log("StoryBool :", storyBool.value);
      return storyBool.value;
    case "cinema":
      console.log("CinemaBool :", cinemaBool.value);
      cinemaBool.value = !cinemaBool.value;
      if (test == "true") {
        card_open.value = !card_open.value;
      }
      console.log("CinemaBool :", cinemaBool.value);
      return cinemaBool.value;
    case "music":
      console.log("MusicBool :", musicBool.value);
      musicBool.value = !musicBool.value;
      if (test == "true") {
        card_open.value = !card_open.value;
      }
      console.log("MusicBool :", musicBool.value);
      return musicBool.value;
  }
};
</script>

<style lang="scss" scoped>
.e-card {
  z-index: 100;
  position: fixed;
  background-color: black;
  width: 100%;
  height: 100vh;
  opacity: 60%;
  top: 0;

  &__content {
    position: fixed;
    width: 80%;
    border-radius: rem(10);
    z-index: 1000;
    top: 20%;
    padding-top: rem(15);
    padding-bottom: rem(15);
    padding-right: rem(20);
    padding-left: rem(20);
  }

  &__script {
    position: fixed;
    width: 80%;
    border-radius: rem(10);
    z-index: 1000;
    color: white;
    background-color: v-bind(couleur2);
    opacity: 100%;
    padding-top: rem(15);
    padding-bottom: rem(15);
    padding-right: rem(20);
    padding-left: rem(20);
  }

  &__title {
    font-family: $secondary-font-family;
    color: v-bind(couleur);
    font-size: $bigger-font-size;
    font-weight: 200;
    margin: rem(0);
    margin-bottom: rem(40);
  }

  &__text {
    font-family: $primary-font-family;
    color: v-bind(couleur);
    font-size: $regular-font-size;
    font-weight: 600;
  }

  &__icons {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: rem(30);
    padding-top: rem(15);
    padding-bottom: rem(15);
    padding-left: rem(25);
  }

  &__button {
    display: flex;
    justify-content: center;
    position: fixed;
    width: 80%;
    z-index: 1000;
    top: 60%;
    margin-top: rem(30);
    padding-top: rem(15);
    padding-bottom: rem(15);
    padding-left: rem(25);
    padding-right: rem(25);
  }
}
</style>
