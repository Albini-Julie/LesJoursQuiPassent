<script setup>
const props = defineProps({
  size: String,
  dimension: Boolean,
  couleur: String,
  href: String,
});

const className = computed(
  () =>
    `button
  ${props.size === "small" ? "-small" : ""}
  ${props.dimension === true ? "-dimension" : ""} `
);
</script>

<template>
  <nuxt-link :to="href">
    <button class="button" size="small" variant="rounded" :class="className">
      <slot></slot>
    </button>
  </nuxt-link>
</template>

<style lang="scss" scoped>
.button {
  border-style: solid;
  border-color: v-bind(couleur);
  border-width: rem(4);
  font-family: $primary-font-family;
  font-size: $bigger-font-size;
  color: v-bind(couleur);
  padding-top: rem(19);
  padding-bottom: rem(19);
  padding-right: rem(30);
  padding-left: rem(30);
  background-color: transparent;
  border-radius: rem(10);

  &.-small {
    border-radius: rem(10);
    font-size: $regular-font-size;
    padding-top: rem(5.5);
    padding-bottom: rem(5.5);
    border-width: rem(2);
  }

  &.-dimension {
    box-shadow: 0;
    box-shadow: 0px 5px 0px v-bind(couleur);
  }
}
</style>
