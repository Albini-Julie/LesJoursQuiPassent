<template>
  <c-header :couleur="secondaryColor" filtre />
  <div class="trait">
    <c-trait :couleur="secondaryColor" />
  </div>
  <h2 class="titleh2">Indiquez votre date de naissance :</h2>
  <div class="input">
    <input id="userDate" type="text" v-model="selectedDate" class="e-input" />
  </div>
  <div class="button">
    <c-bouton :couleur="secondaryColor" href="/donnees">Commencer</c-bouton>
  </div>
  <div class="button --little">
    <c-bouton size="small" :couleur="secondaryColor" href="/donnees"
      >Commencer</c-bouton
    >
  </div>
  <c-footer :couleur="secondaryColor" />
</template>

<script>
import { ref, onMounted, onUnmounted } from "vue";
import flatpickr from "flatpickr";
import "/flatpickr.min.css";
import { French } from "flatpickr/dist/l10n/fr.js";

export default {
  setup() {
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
    };

    onMounted(() => {
      setColor();
      flatpickr("#userDate", {
        // Options de configuration de flatpickr
        dateFormat: "d F Y", // Format de la date
        minDate: "1930-01-01", // Date minimale
        defaultDate: new Date(), // Date par défaut
        locale: French,
      });
    });

    onUnmounted(() => {
      setColor();
    });
    return {
      primaryColor,
      secondaryColor,
      selectedDate: "",
    };
  },
};
</script>

<style lang="scss" scoped>
.trait {
  display: flex;
  justify-content: center;
  margin-top: 60px;
  margin-bottom: 70px;
}

.titleh2 {
  font-family: $primary-font-family;
  font-size: $big-font-size;
  display: flex;
  justify-content: center;
  color: v-bind(secondaryColor);
  margin-bottom: 75px;
  text-align: center;
  @include medium-up {
    font-size: $bigger-font-size;
  }
  @include large-up {
    margin-bottom: 200px;
    text-align: start;
  }
}

.input {
  display: flex;
  justify-content: center;
}
.button {
  display: flex;
  justify-content: center;
  margin-bottom: rem(70);
  display: none;
  @include medium-up {
    display: flex;
  }

  &.--little {
    display: flex;
    @include medium-up {
      display: none;
    }
  }
}
.e-input {
  @include only-small {
    width: 80%;
  }
  background-color: v-bind(primaryColor);
  border: none;
  border-bottom: solid;
  border-width: 2px;
  border-color: v-bind(secondaryColor);
  font-size: $bigger-font-size;
  margin-bottom: rem(100);
  color: v-bind(secondaryColor);
  font-family: $secondary-font-family;
  text-align: center;
  @include medium-up {
    margin-bottom: rem(150);
  }

  &:focus {
    outline: none;
  }
}
</style>
