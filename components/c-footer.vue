<script setup>
defineProps({
  couleur: String,
});
</script>

<template>
  <div class="footer">
    <a class="e-footer__link" href="/mentionslegales"
      ><p class="e-footer__text">mentions légales</p></a
    >
    <a class="e-footer__link" href="/apropos"
      ><p class="e-footer__text">à propos</p></a
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
