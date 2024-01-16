<script>
import { ref, onMounted, onUnmounted } from "vue";
import { filter_open } from "@/config.js";

export default {
  props: {
    filtre: Boolean,
    croix: Boolean,
    couleur: String,
  },

  setup(props) {
    const primaryColor = ref("");
    const secondaryColor = ref("");
    const icons = ref("");

    const setColor = () => {
      const date = new Date();
      const day = date.getDate();
      const month = date.getMonth() + 1;

      if ((month === 12 && day >= 21) || month === 1 || month === 2 || (month === 3 && day < 21)) {
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

    const funcFilter = () => {
      filter_open.value = !filter_open.value;
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
      funcFilter,
    };
  },
};
</script>

<template>
  <div class="header">
    <nuxt-link class="e-header__link" to="/"><logo_2 :couleur="secondaryColor" /></nuxt-link>
    <automn class="e-header__icon" v-if="icons === 'automn'" :couleur="secondaryColor" />
    <spring class="e-header__icon" v-else-if="icons === 'spring'" :couleur="secondaryColor" />
    <summer class="e-header__icon" v-else-if="icons === 'summer'" :couleur="secondaryColor" />
    <winter class="e-header__icon" v-else-if="icons === 'winter'" :couleur="secondaryColor" />
    <croix
      v-if="croix"
      @click="funcFilter"
      class="e-header__icon --phone"
      :couleur="secondaryColor" />
    <filtre
      @click="funcFilter"
      v-else-if="filtre"
      class="e-header__icon --phone"
      :couleur="secondaryColor" />
    <croix :couleur="primaryColor" class="e-header__icon" />
  </div>
  <div class="e-header__boxicons">
    <automn class="e-header__icon --phone" v-if="icons === 'automn'" :couleur="secondaryColor" />
    <spring
      class="e-header__icon --phone"
      v-else-if="icons === 'spring'"
      :couleur="secondaryColor" />
    <summer
      class="e-header__icon --phone"
      v-else-if="icons === 'summer'"
      :couleur="secondaryColor" />
    <winter
      class="e-header__icon --phone"
      v-else-if="icons === 'winter'"
      :couleur="secondaryColor" />
  </div>
</template>

<style lang="scss" scoped>
.header {
  display: flex;
  justify-content: space-between;
  padding: rem(25);
  align-items: center;
}

.e-header {
  &__link {
    text-decoration: none;
  }

  &__boxicons {
    display: flex;
    justify-content: center;
  }

  &__icon {
    display: block;
    position: absolute;
    left: 50%;
    transform: translateX(-50%);

    @include only-small {
      display: none;
    }
    &.--phone {
      display: none;
      @include only-small {
        display: block;
      }
    }
  }
}
</style>
~/config.js
