<script setup>
defineProps({
  couleur: String,
});
</script>

<template>
  <div class="logo">
    <p class="e-logo__text">Les jours</p>
    <p class="e-logo__text">qui passent .</p>
  </div>
</template>

<style lang="scss" scoped>
.logo {
  border: solid;
  border-color: v-bind(couleur);
  border-width: rem(1.25);
  border-radius: rem(6.55);
  width: fit-content;
  padding-top: rem(8);
  padding-bottom: rem(8);
  padding-left: rem(10);
  padding-right: rem(10);
}

.e-logo__text {
  font-family: $secondary-font-family;
  color: v-bind(couleur);
  margin: 0px;
}
</style>
