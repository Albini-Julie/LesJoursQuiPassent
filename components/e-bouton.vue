<script setup>
const props = defineProps({
  size: String,
  dimension: Boolean,
  couleur: String,
});

//Création d'une constante className qui va retourner un nom de classe différent selon la valeur des propriétés variant, size et icon
const className = computed(
  () =>
    `button
  ${props.size === "small" ? "-small" : ""}
  ${props.dimension === true ? "-dimension" : ""} `
);
</script>

<template>
  <button class="button" size="small" variant="rounded" :class="className">
    <slot></slot>
  </button>
</template>

<style lang="scss" scoped>
.button {
  border-style: solid;
  border-color: blue;
  border-width: rem(4);
  font-family: $primary-font-familly;
  font-size: $bigger-font-size;
  color: blue;
  padding-top: rem(19);
  padding-bottom: rem(19);
  padding-right: rem(30);
  padding-left: rem(30);
  background-color: none;
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
    box-shadow: 0px 5px 0px blue;
  }
}
</style>
