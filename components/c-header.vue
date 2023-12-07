<template>
  <div class="header">
    <!--Logo du site-->
    <logo_2 :couleur="secondaryColor" />
    <!--Logo de la saison-->
    <automn v-if="icons === 'automn'" :couleur="secondaryColor" />
    <spring v-else-if="icons === 'spring'" :couleur="secondaryColor" />
    <summer v-else-if="icons === 'summer'" :couleur="secondaryColor" />
    <winter v-else-if="icons === 'winter'" :couleur="secondaryColor" />
    <!--Logo en plus-->
    <croix v-if="filtre === false && croix === false" :couleur="primaryColor" />
    <croix
      v-if="filtre === false && croix === true"
      :couleur="secondaryColor"
    />
    <filtre
      v-if="filtre === true && croix === true"
      :couleur="secondaryColor"
    />
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted, defineProps } from "vue";

defineProps({
  filtre: Boolean,
  croix: Boolean,
});

export default {
  setup() {
    const primaryColor = ref("");
    const secondaryColor = ref("");
    const icons = ref("");

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
        icons.value = "winter";
      } else if (
        (month === 3 && day >= 21) ||
        month === 4 ||
        (month === 5 && day <= 20) ||
        (month === 6 && day < 21)
      ) {
        primaryColor.value = "#2E3E1A";
        secondaryColor.value = "#D398EF";
        icons.value = "spring";
      } else if (
        (month === 6 && day >= 21) ||
        month === 7 ||
        month === 8 ||
        (month === 9 && day < 21)
      ) {
        primaryColor.value = "#D09C14";
        secondaryColor.value = "#FFFFFF";
        icons.value = "summer";
      } else if (
        (month === 9 && day >= 21) ||
        month === 10 ||
        month === 11 ||
        (month === 12 && day < 21)
      ) {
        primaryColor.value = "#391B0A";
        secondaryColor.value = "#DE8706";
        icons.value = "automn";
      }
    };

    onMounted(() => {
      setColor();
    });

    onUnmounted(() => {
      setColor();
    });
    return {
      primaryColor,
      secondaryColor,
      icons,
    };
  },
};
</script>

<style lang="scss" scoped>
.header {
  display: flex;
  justify-content: space-between;
  padding: rem(25);
}
</style>
