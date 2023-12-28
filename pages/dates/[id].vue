<template>
  <!--Header-->
  <c-header filtre />
  <div class="e-id__trait">
    <c-trait
      :couleur="secondaryColor"
      :year="yearFromURL"
      :day="dayFromURL"
      :month="monthFromURL"
    />
  </div>
  <!--Timer-->
  <c-timer
    :year="yearFromURL"
    :day="dayFromURL"
    :month="monthFromURL_before"
    :couleur="secondaryColor"
    class="e-id__timer"
  />
  <!--Fleurs de filtrage-->
  <div class="e-id__fleurs">
    <div class="e-id__fleurs --semieronde2">
      <fleur_semieronde2 @click="toggleNazaBool" :couleur="secondaryColor" />
    </div>
    <div class="e-id__fleurs --pointue">
      <fleur_pointue :couleur="secondaryColor" />
    </div>
    <div class="e-id__fleurs --semieronde">
      <fleur_semieronde :couleur="secondaryColor" />
    </div>
    <div class="e-id__fleurs --ronde">
      <fleur_ronde :couleur="secondaryColor" />
    </div>
  </div>
  <!--Picture of the day-->
  <div v-if="apodData && nazaBool">
    <h3>{{ apodData.title }}</h3>
    <p>{{ apodData.explanation }}</p>
    <img :src="apodData.url" alt="NASA APOD" />
  </div>
  <!--Calculateur d'âge-->
  <c-age
    :year="yearFromURL"
    :month="monthFromURL_before"
    :day="dayFromURL"
    :couleur="secondaryColor"
    class="e-id__age"
  />

  <!--Fenetre des filtres-->
  <div
    class="e-filter"
    :class="{
      visible: isFilterOpen(),
      animation: isFilterOpen(),
      inverse: !isFilterOpen(),
    }"
  >
    <!-- Contenu de la fenêtre -->
    <c-header croix :couleur="secondaryColor" />
    <div class="e-id__trait">
      <c-trait
        :couleur="secondaryColor"
        :year="yearFromURL"
        :day="dayFromURL"
        :month="monthFromURL"
      />
    </div>
    <p class="e-filter__text">Choisissez une catégorie d’évènement</p>
    <div class="e-filter__Blockflowers">
      <fleur_semieronde2
        @click="toggleNazaBool"
        class="e-filter__flowers"
        :couleur="secondaryColor"
      />
      <fleur_pointue class="e-filter__flowers" :couleur="secondaryColor" />
    </div>
    <div class="e-filter__Blockflowers">
      <fleur_semieronde class="e-filter__flowers" :couleur="secondaryColor" />
      <fleur_ronde class="e-filter__flowers" :couleur="secondaryColor" />
    </div>
  </div>

  <c-footer :couleur="secondaryColor" class="e-id__footer" />
</template>

<style lang="scss" scoped>
.e-id {
  &__trait {
    display: flex;
    justify-content: center;
    margin-top: 60px;
    margin-bottom: 20px;
    @include large-up {
      margin-bottom: 70px;
    }
  }

  &__timer {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    margin-left: rem(20);
    margin-right: rem(20);
    @include x-large-up {
      margin: 0px;
    }
  }

  &__age {
    margin-top: 130px;
    display: flex;
    justify-content: center;
    @include large-up {
      margin-top: 100px;
    }
  }

  &__fleurs {
    justify-content: center;
    margin-top: rem(60);
    gap: rem(33);
    display: none;
    @include medium-up {
      display: flex;
    }

    &.--semieronde2:hover::before {
      /* Afficher le message au survol */
      content: "Image of the day by NAZA";
      display: block;
      position: absolute;
      background-color: v-bind(primaryColor);
      color: v-bind(secondaryColor);
      border: solid;
      border-width: rem(1);
      border-color: v-bind(secondaryColor);
      font-family: $primary-font-family;
      font-weight: 500;
      padding: 5px;
      border-radius: 5px;
      margin-top: -25px; /* Ajustez la position du message selon vos besoins */
      margin-left: 10px;
      z-index: 1; /* Assurez-vous que le message est au-dessus de l'élément */
      margin-top: rem(-40);
    }
    &.--semieronde:hover::before {
      /* Afficher le message au survol */
      content: "Cinéma";
      display: block;
      position: absolute;
      background-color: v-bind(primaryColor);
      color: v-bind(secondaryColor);
      border: solid;
      border-width: rem(1);
      border-color: v-bind(secondaryColor);
      font-family: $primary-font-family;
      font-weight: 500;
      padding: 5px;
      border-radius: 5px;
      margin-top: -25px; /* Ajustez la position du message selon vos besoins */
      margin-left: 10px;
      z-index: 1; /* Assurez-vous que le message est au-dessus de l'élément */
      margin-top: rem(-40);
    }
    &.--ronde:hover::before {
      /* Afficher le message au survol */
      content: "Musique";
      display: block;
      position: absolute;
      background-color: v-bind(primaryColor);
      color: v-bind(secondaryColor);
      border: solid;
      border-width: rem(1);
      border-color: v-bind(secondaryColor);
      font-family: $primary-font-family;
      font-weight: 500;
      padding: 5px;
      border-radius: 5px;
      margin-top: -25px; /* Ajustez la position du message selon vos besoins */
      margin-left: 10px;
      z-index: 1; /* Assurez-vous que le message est au-dessus de l'élément */
      margin-top: rem(-40);
    }
    &.--pointue:hover::before {
      /* Afficher le message au survol */
      content: "Histoire";
      display: block;
      position: absolute;
      background-color: v-bind(primaryColor);
      color: v-bind(secondaryColor);
      border: solid;
      border-width: rem(1);
      border-color: v-bind(secondaryColor);
      font-family: $primary-font-family;
      font-weight: 500;
      padding: 5px;
      border-radius: 5px;
      margin-top: -25px; /* Ajustez la position du message selon vos besoins */
      margin-left: 10px;
      z-index: 1; /* Assurez-vous que le message est au-dessus de l'élément */
      margin-top: rem(-40);
    }
  }

  &__footer {
    margin-top: rem(20);
  }
}

//Style de la fenêtre des filtres
.e-filter {
  position: fixed;
  z-index: 50;
  background-color: v-bind(primaryColor);
  width: 100%;
  height: 100vh;
  @include medium-up {
    display: none;
  }

  &__text {
    text-align: center;
    color: v-bind(secondaryColor);
    font-family: $primary-font-family;
    font-size: $medium-font-size;
  }

  &__Blockflowers {
    margin-top: rem(40);
    display: flex;
    justify-content: center;
    gap: rem(50);
  }

  &__flowers {
    width: rem(125);
    height: rem(125);
  }
}

.visible {
  top: 0; /* Déplacez la fenêtre vers le haut pour la rendre visible */
}

.animation {
  animation: aller 2s;
}

@keyframes aller {
  from {
    transform: translateY(100%);
  }
  to {
    transform: translateY(0);
  }
}

.inverse {
  animation: retour 2s;
}

@keyframes retour {
  from {
    transform: translateY(-100%);
  }
  to {
    transform: translateY(0);
  }
}
</style>

<script>
import axios from "axios";
import { ref, onMounted, onUnmounted } from "vue";
import { filter_open } from "@/config.js";

export default {
  setup() {
    // Variables de données
    const apodData = ref(null);
    const dateFromURL = ref(null);
    const nazaBool = ref(true);

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

    const toggleNazaBool = () => {
      nazaBool.value = !nazaBool.value;
      console.log(nazaBool.value);
    };

    const isFilterOpen = () => {
      return filter_open.value === true;
    };

    onMounted(() => {
      setColor();
      console.log(filter_open.value);
    });

    onUnmounted(() => {
      setColor();
    });

    return {
      apodData,
      dateFromURL,
      nazaBool,
      primaryColor,
      secondaryColor,
      dayGet,
      monthF,
      yearGet,
      toggleNazaBool,
      isFilterOpen,
    };
  },

  // Récupération de l'image du jour
  mounted() {
    // Récupérer l'URL complète
    const urlString = window.location.href;
    const url = new URL(urlString);

    // Accéder au chemin (pathname) de l'URL
    const pathname = url.pathname;

    // Utiliser une expression régulière pour extraire la date du chemin
    const match = pathname.match(/\/dates\/(\d{4}-\d{2}-\d{2})/);

    // Vérifier si la correspondance a réussi et récupérer la date
    this.dateFromURL = match ? match[1] : null;

    // Décomposer la date en année, mois et jour
    if (this.dateFromURL) {
      const [year, month, day] = this.dateFromURL.split("-");
      this.yearFromURL = parseInt(year, 10);
      this.monthFromURL_before = parseInt(month, 10);
      this.dayFromURL = parseInt(day, 10);

      if (this.monthFromURL_before == 1) {
        this.monthFromURL = "Janvier";
      } else if (this.monthFromURL_before == 2) {
        this.monthFromURL = "Février";
      } else if (this.monthFromURL_before == 3) {
        this.monthFromURL = "Mars";
      } else if (this.monthFromURL_before == 4) {
        this.monthFromURL = "Avril";
      } else if (this.monthFromURL_before == 5) {
        this.monthFromURL = "Mai";
      } else if (this.monthFromURL_before == 6) {
        this.monthFromURL = "Juin";
      } else if (this.monthFromURL_before == 7) {
        this.monthFromURL = "Juillet";
      } else if (this.monthFromURL_before == 8) {
        this.monthFromURL = "Août";
      } else if (this.monthFromURL_before == 9) {
        this.monthFromURL = "Septembre";
      } else if (this.monthFromURL_before == 10) {
        this.monthFromURL = "Octobre";
      } else if (this.monthFromURL_before == 11) {
        this.monthFromURL = "Novembre";
      } else {
        this.monthFromURL = "Décembre";
      }

      // Appeler la méthode fetchApod après avoir récupéré la date
      this.fetchApod();
    }
  },
  methods: {
    async fetchApod() {
      try {
        if (this.dateFromURL) {
          const response = await axios.get(
            `https://api.nasa.gov/planetary/apod?api_key=DEMO_KEY&date=${this.dateFromURL}`
          );
          this.apodData = response.data;
        }
      } catch (error) {
        console.error("Error fetching APOD:", error);
        this.apodData = null;
      }
    },
  },
};
</script>
