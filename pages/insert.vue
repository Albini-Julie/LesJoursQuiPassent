<template>
  <c-header :couleur="secondaryColor" />
  <div class="trait">
    <c-trait :couleur="secondaryColor" />
  </div>
  <h2 class="titleh2">Indiquez votre date de naissance :</h2>
  <input
    id="userDate"
    type="text"
    v-model="selectedDate"
    placeholder="Sélectionnez une date"
    class="flatpickr-input"
  />
</template>

<script>
import { ref, onMounted, onUnmounted } from "vue";
import flatpickr from "flatpickr";
import "/flatpickr.min.css";

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
        dateFormat: "Y-m-d", // Format de la date
        minDate: "1930-01-01", // Date minimale
        defaultDate: new Date(), // Date par défaut
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
  font-size: $bigger-font-size;
  display: flex;
  justify-content: center;
  color: v-bind(secondaryColor);
  @include large-up {
    margin-bottom: 200px;
  }
}

.input {
}
</style>
