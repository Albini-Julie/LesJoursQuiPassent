<template>
  <div class="app-container">
    <NuxtLayout />
  </div>
</template>

<style lang="scss">
.app-container {
  min-height: 100vh;
  background-color: v-bind(primaryColor);
  margin: 0;
  padding: 0;
}
</style>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from "vue";

const primaryColor = ref("");
const secondaryColor = ref("");

const setColor = () => {
  const date = new Date();
  const day = date.getDate();
  const month = date.getMonth() + 1;

  if (
    (month === 12 && day >= 21) ||
    month === 1 ||
    month === 2 ||
    (month === 3 && day < 21)
  ) {
    primaryColor.value = "#FFFFFF";
    secondaryColor.value = "#4359AA";
  } else if (
    (month === 3 && day >= 21) ||
    month === 4 ||
    (month === 5 && day <= 20) ||
    (month === 6 && day < 21)
  ) {
    primaryColor.value = "#2E3E1A";
    secondaryColor.value = "#D398EF";
  } else if (
    (month === 6 && day >= 21) ||
    month === 7 ||
    month === 8 ||
    (month === 9 && day < 21)
  ) {
    primaryColor.value = "#D09C14";
    secondaryColor.value = "#FFFFFF";
  } else if (
    (month === 9 && day >= 21) ||
    month === 10 ||
    month === 11 ||
    (month === 12 && day < 21)
  ) {
    primaryColor.value = "#391B0A";
    secondaryColor.value = "#DE8706";
  }

  onMounted(() => {
    setColor();
  });

  onUnmounted(() => {
    setColor();
  });

  useSeoMeta({
    title: "Les jours qui passent",
    ogTitle: "Les jours qui passent",
    description:
      "Les jours qui passent est un site poétique permettant de changer sa vision du temps en ayant accès à des données uniques sur une date particulière.",
    ogDescription:
      "Les jours qui passent est un site poétique permettant de changer sa vision du temps en ayant accès à des données uniques sur une date particulière.",
    ogImage: "/Logo_LesJoursQuiPassent.jpg",
    twitterCard: "summary_large_image",
    keywords:
      "temps, découverte, date, jour, mois, année, événements historiques, histoire, NASA, proverbe, citation, films, cinema, poétique, saisons",
  });

  return {
    primaryColor,
    secondaryColor,
  };
};
</script>
