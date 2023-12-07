<script setup>
defineProps({
  couleur: String,
});
</script>

<template>
  <div class="footer">
    <nuxt-link class="e-footer__link" to="/mentionslegales"
      ><p class="e-footer__text">mentions légales</p></nuxt-link
    >
    <nuxt-link class="e-footer__link" to="/apropos"
      ><p class="e-footer__text">à propos</p></nuxt-link
    >
  </div>
</template>

<style lang="scss" scoped>
.footer {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  padding-bottom: 20px;
}
.e-footer {
  &__text {
    color: v-bind(couleur);
    font-family: $primary-font-family;
    font-size: $small-font-size;
    margin: 0px;
  }

  &__link {
    text-decoration: none;
  }
}
</style>
