<template>
  <c-header :couleur="secondaryColor" />
  <!--Date du jour-->
  <div class="trait">
    <c-trait
      :couleur="secondaryColor"
      :day="dayGet"
      :month="monthF"
      :year="yearGet"
    />
  </div>

  <!--Citation-->
  <div class="quote">
    <p class="quote__content">
      <apostrophe class="quote__apo" :couleur="secondaryColor" />
      <p class="quote__text">{{ quoteText }}</p>
      <apostrophe class="quote__apo" :couleur="secondaryColor" />
    </p>
    <div class="quote__author">
      <p class="quote__text">{{ quoteAuthor }}</p>
    </div>
  </div>
  <!--Titre-->
  <h2 class="titleh2">Indiquez votre date de naissance :</h2>
  <!--Champ d'entrée-->
  <div class="input">
    <input
      type="text"
      v-model="selectedDate"
      class="e-input"
      placeholder="année-mois-jour"
    />
  </div>
  <!--Boutons-->
  <div class="button">
    <c-bouton
      :couleur="secondaryColor"
      @click="redirectToDatesPage(selectedDate)"
      >Commencer</c-bouton
    >
  </div>
  <div class="button --little">
    <c-bouton
      size="small"
      :couleur="secondaryColor"
      @click="redirectToDatesPage(selectedDate)"
      >Commencer</c-bouton
    >
  </div>
  <!--Footer-->
  <c-footer :couleur="secondaryColor" />
</template>

<script>
import { ref, onMounted, onUnmounted } from "vue";

export default {
  setup() {
    const quoteText = ref("");
    const quoteAuthor = ref("");
    //Fonction citation
    const fetchDataFromApi = async () => {
      try {
        const response = await fetch("https://api.quotable.io/random");
        const quote = await response.json();

        // Output the quote and author name
        quoteText.value = quote.content;
        quoteAuthor.value = quote.author;
        console.log(quote.content);
        console.log(`- ${quote.author}`);
      } catch (error) {
        console.error("Error fetching random quote:", error);
      }
    };
    //redirection vers la page de la date
    function redirectToDatesPage(date) {
      console.log(date);
      const userInput = date; // Remplacez cela par la valeur de votre champ de saisie
      if (isValidDate(userInput)) {
        const url = `/dates/${date}`;
        // Effectuer la redirection
        window.location.href = url;
      } else {
        // Fenêtre d'alerte personnalisée
        const errorMessage = "La date n'est pas valide.";
        const alertStyle = "background-color: #8B0000; color: #FFFFFF;";

        // Afficher la fenêtre d'alerte personnalisée
        showAlert(errorMessage, alertStyle);
      }
    }

    function showAlert(message, style) {
      const alertContainer = document.createElement("div");
      alertContainer.style = `
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    padding: 15px;
    border-radius: 5px;
    font-family: Urbanist;
    ${style}`;

      const alertMessage = document.createElement("p");
      alertMessage.textContent = message;

      alertContainer.appendChild(alertMessage);
      document.body.appendChild(alertContainer);

      // Supprimer la fenêtre d'alerte après un certain délai (par exemple, 3 secondes)
      setTimeout(() => {
        document.body.removeChild(alertContainer);
      }, 3000);
    }

    function isValidDate(dateString) {
      const dateObject = new Date(dateString);

      // Vérifier si la conversion a réussi et que la date reste valide
      const isDateValid = !isNaN(dateObject.getTime());

      // Vérifier si l'année est entre 1930 et l'année actuelle
      const isYearValid =
        dateObject.getFullYear() >= 1930 &&
        dateObject.getFullYear() <= new Date().getFullYear();

      return isDateValid && isYearValid;
    }

    // Couleur Secondary et Primary selon les saisons

    const primaryColor = ref("");
    const secondaryColor = ref("");
    const dateGet = new Date();
    const dayGet = dateGet.getDate();
    const monthGet = dateGet.getMonth() + 1;
    const monthF = ref("");
    const yearGet = dateGet.getFullYear();

    if (monthGet == 1) {
      monthF.value = "Janvier";
    } else if (monthGet == 2) {
      monthF.value = "Février";
    } else if (monthGet == 3) {
      monthF.value = "Mars";
    } else if (monthGet == 4) {
      monthF.value = "Avril";
    } else if (monthGet == 5) {
      monthF.value = "Mai";
    } else if (monthGet == 6) {
      monthF.value = "Juin";
    } else if (monthGet == 7) {
      monthF.value = "Juillet";
    } else if (monthGet == 8) {
      monthF.value = "Août";
    } else if (monthGet == 9) {
      monthF.value = "Septembre";
    } else if (monthGet == 10) {
      monthF.value = "Octobre";
    } else if (monthGet == 11) {
      monthF.value = "Novembre";
    } else {
      monthF.value = "Décembre";
    }

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
      fetchDataFromApi();
    });

    onUnmounted(() => {
      setColor();
      fetchDataFromApi();
    });
    return {
      primaryColor,
      secondaryColor,
      selectedDate: "",
      dayGet,
      monthF,
      yearGet,
      redirectToDatesPage,
      quoteText,
      quoteAuthor,
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
  font-weight: 300;
  @include medium-up {
    font-size: $bigger-font-size;
    font-weight: 600;
  }
  @include large-up {
    margin-bottom: 200px;
    text-align: start;
  }
}

.input {
  display: flex;
  justify-content: center;

  ::placeholder {
    font-family: $primary-font-family;
    color: v-bind(secondaryColor);
    opacity: 0.4;
  }
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

.quote {
  display: flex;
  flex-direction: column;
  align-items: center;
  

  &__content {
    display: flex;  
    gap:20px;
    justify-content: center;
    margin-right: rem(20);
    margin-left: rem(20);
    @include medium-up{
      margin-left:50px;
      margin-right:50px
    }
    @include large-up{
      margin-left:100px;
      margin-right:100px
    }
    @include x-large-up {
      margin-left:0px;
      margin-right:0px;
      text-align: start;
      margin-right: 0;
      margin-left: 0;
      width: 80%;
    }
  }

  &__apo {
     display: none;
    @include medium-up {
      display: block;
    }
    @include large-up {
      
    }
    @include x-large-up {
      
    }
  }

  &__text {
    font-family: $primary-font-family;
    font-size: $regular-font-size;
    color: v-bind(secondaryColor);
    @include medium-up {
      font-size: $medium-font-size;
    }
    @include large-up {
      font-size: $big-font-size;
    }

    &.--size {
      font-size: $medium-font-size;
      @include medium-up {
        font-size: $big-font-size;
      }
      @include large-up {
        font-size: $bigger-font-size;
      }
    }
  }

  &__author {
    display: flex;
    justify-content: flex-end;
    width: 70%;
  }
}
</style>
