<script>
import axios from "axios";
import { ref, onMounted, onUnmounted } from "vue";
import { filter_open } from "@/config.js";
import { card_open } from "@/config.js";
import { nazaBool, storyBool, cinemaBool, musicBool } from "@/config.js";

export default {
  data() {
    return {
      // Supposons que vous avez plusieurs films, chaque propriété est un booléen indiquant si le contenu est visible
      contentVisible: {},
    };
  },
  setup() {
    // Variables de données
    const apodData = ref(null);
    const dateFromURL = ref(null);

    const FilterChoice = ref("");
    const FilterChoiceOpen = ref(false);

    // Couleur Secondary et Primary selon les saisons
    const primaryColor = ref("");
    const secondaryColor = ref("");
    const dateGet = new Date();
    const dayGet = dateGet.getDate();
    const monthGet = dateGet.getMonth() + 1;
    const monthF = ref("");
    const yearGet = dateGet.getFullYear();
    const movies = [];
    const history = [];
    const imageBaseURL = "https://image.tmdb.org/t/p/w500"; // Base URL for movie images

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

    const toggleBool = (theme, test) => {
      switch (theme) {
        case "naza":
          console.log("NazaBool :", nazaBool.value);
          nazaBool.value = !nazaBool.value;
          if (test == "true") {
            card_open.value = !card_open.value;
          }
          console.log("NazaBool :", nazaBool.value);
          return nazaBool.value;
        case "story":
          console.log("StoryBool :", storyBool.value);
          storyBool.value = !storyBool.value;
          if (test == "true") {
            card_open.value = !card_open.value;
          }
          console.log("StoryBool :", storyBool.value);
          return storyBool.value;
        case "cinema":
          console.log("CinemaBool :", cinemaBool.value);
          cinemaBool.value = !cinemaBool.value;
          if (test == "true") {
            card_open.value = !card_open.value;
          }
          console.log("CinemaBool :", cinemaBool.value);
          return cinemaBool.value;
        case "music":
          console.log("MusicBool :", musicBool.value);
          musicBool.value = !musicBool.value;
          if (test == "true") {
            card_open.value = !card_open.value;
          }
          console.log("MusicBool :", musicBool.value);
          return musicBool.value;
      }
    };

    const isFilterOpen = () => {
      return filter_open.value === true;
    };

    // Ajoutez une méthode pour inverser la valeur de Card_open
    const inverserCardOpen = (num) => {
      card_open.value = !card_open.value;
      switch (num) {
        case 1:
          FilterChoice.value = "naza";
          console.log(
            "FilterChoice: ",
            FilterChoiceOpen.value,
            "Card_open: ",
            card_open.value
          );
          return card_open.value;
          break;
        case 2:
          FilterChoice.value = "histoire";
          console.log(
            "FilterChoice: ",
            FilterChoiceOpen.value,
            "Card_open: ",
            card_open.value
          );
          return card_open.value;
          break;
        case 3:
          FilterChoice.value = "cinema";

          console.log(
            "FilterChoice: ",
            FilterChoiceOpen.value,
            "Card_open: ",
            card_open.value
          );
          return card_open.value;
          break;
        case 4:
          FilterChoice.value = "musique";
          console.log(
            "FilterChoice: ",
            FilterChoiceOpen.value,
            "Card_open: ",
            card_open.value
          );
          return card_open.value;
          break;
      }
      return card_open.value;
    };

    onMounted(() => {
      setColor();
    });

    onUnmounted(() => {
      setColor();
    });

    return {
      apodData,
      dateFromURL,
      nazaBool,
      cinemaBool,
      storyBool,
      primaryColor,
      secondaryColor,
      dayGet,
      monthF,
      yearGet,
      toggleBool,
      isFilterOpen,

      FilterChoice,
      inverserCardOpen,
      card_open,
    };
  },

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

      // Ajoutez des déclarations de console.log pour déboguer
      console.log("Year:", this.yearFromURL);
      console.log("Month before:", this.monthFromURL_before);
      console.log("Day:", this.dayFromURL);

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
      this.fetchMovies(); // Ensure that fetchMovies is called only when dateFromURL is defined
      this.fetchApod();
      this.fetchDB();
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

    async fetchMovies() {
      try {
        const response = await axios.get(
          `https://api.themoviedb.org/3/discover/movie?api_key=8e0a1d9f7eb0d1d657ea7de87fd35e87&primary_release_year=${this.yearFromURL}&language=fr-FR`
        );
        this.movies = response.data.results;
        console.log(this.movies);
      } catch (error) {
        console.error("Error fetching movies:", error);
        this.movies = [];
      }
    },
    getImageUrl(path) {
      return path ? `https://image.tmdb.org/t/p/w500${path}` : "";
    },
    /*getImageUrl(path) {
      const urlString = window.location.href;
      const url = new URL(urlString);
      return path ? url + path : ""; // Concatenate with base URL
      //return path ? this.imageBaseURL + path : ""; // Concatenate with base URL
    },*/
    async fetchDB() {
      try {
        console.log(
          `/${this.dayFromURL}/${this.monthFromURL_before}/${this.yearFromURL}`
        );
        const response = await axios.get(
          `https://api.ext.abzk.fr/search/${this.dayFromURL}/${this.monthFromURL_before}/${this.yearFromURL}`
        );

        this.history = response.data;
        console.log(this.history);
      } catch (error) {
        console.error("Error fetching history:", error);
        this.history = [];
      }
    },

    copyPageUrl() {
      const url = window.location.href;
      navigator.clipboard
        .writeText(url)
        .then(() => {
          alert("Lien copié dans le presse-papiers !");
        })
        .catch((err) => {
          console.error("Erreur lors de la copie du lien : ", err);
        });
    },
  },
};
</script>

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
      <fleur_semieronde2
        id="1"
        @click="toggleBool('naza', 'false')"
        :couleur="secondaryColor"
      />
    </div>
    <div class="e-id__fleurs --pointue">
      <fleur_pointue
        id="2"
        @click="toggleBool('story', 'false')"
        :couleur="secondaryColor"
      />
    </div>
    <div class="e-id__fleurs --semieronde">
      <fleur_semieronde
        id="3"
        @click="toggleBool('cinema', 'false')"
        :couleur="secondaryColor"
      />
    </div>
  </div>
  <p class="histoire__ctnSubtitle --title">
    Cliquez sur les fleurs pour filtrer les données
  </p>

  <!--Picture of the day-->
  <div v-if="apodData && nazaBool" class="APOD">
    <img class="APOD__img" :src="apodData.url" alt="NASA APOD" />
    <div>
      <h1 class="APOD__title">Image of the day</h1>
      <h3 class="APOD__name">
        <a
          :href="
            'https://www.google.com/search?q=' +
            encodeURIComponent(apodData.title)
          "
          target="_blank"
          >{{ apodData.title }}</a
        >
      </h3>

      <p class="APOD__txt">{{ apodData.explanation }}</p>
    </div>
  </div>

  <!--Events DB-->
  <div>
    <div v-if="history && storyBool" class="histoire">
      <h1 class="histoire__ctnTitle">
        Ce qu'il s'est passé le jour de votre naissance
      </h1>
      <p class="histoire__ctnSubtitle">Faites défilez horizontalement</p>
      <div class="scroll__container">
        <div v-for="event in history" :key="event.id" class="scroll__item">
          <div
            style="display: flex; justify-content: flex-end; position: relative"
          >
            <svg
              style="position: absolute; top: 50%; transform: translateY(-50%)"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 1380.5 144.22"
            >
              <path
                class="cls-1"
                d="M12.52,80.1c25.87-30.14,61.5-49.9,100.86-55.58,43.34-6.25,83.95,6.07,121.81,26.54,41.54,22.46,82.35,45.53,126.45,62.79,43.77,17.14,90.04,28.85,137.19,30.22,98.6,2.86,191.3-38.75,283.79-66.94,49.28-15.02,99.12-28.11,149-41.01,48.38-12.51,99.32-28.06,149.71-19.1,44.81,7.96,84.41,31.58,125.39,50.02,20.67,9.3,41.68,17.43,64.13,21.19,23.15,3.88,46.62,4.08,69.87.93,11.67-1.58,23.16-3.99,34.49-7.15,9.28-2.59,5.34-17.07-3.99-14.46-46.7,13.03-95.3,11.62-140.45-6.42-41.86-16.73-80.59-41.04-124.13-53.58-48.64-14.01-97.53-6.44-145.72,5.56s-99.67,25.51-149.08,39.72c-48.64,13.99-96.3,30.77-144.52,46.08-46.55,14.78-94.33,27.63-143.34,29.92-97.88,4.58-187.07-38.24-270.38-84.75-20.25-11.3-40.96-22.19-63.33-28.67-19.01-5.51-39.04-8.1-58.82-7.44-39.45,1.31-77.64,15.37-108.17,40.44-7.76,6.37-14.85,13.45-21.39,21.07s4.31,17.95,10.61,10.61h0Z"
                :fill="secondaryColor"
              />
            </svg>
            <fleur_pointue
              class="histoire__flower"
              id="2"
              :couleur="secondaryColor"
              style="width: 300px; height: 300px"
            />
          </div>
          <div class="histoire__content">
            <div>
              <div class="histoire__subText">
                <p class="histoire__subText--1">
                  ... durant l'année {{ event.annee }}
                </p>
                <p
                  class="histoire__subText--2"
                  v-if="this.yearFromURL - event.annee < 0"
                >
                  vers le moment de vos {{ event.annee - this.yearFromURL }} ans
                </p>
                <p
                  class="histoire__subText--3"
                  v-if="this.yearFromURL - event.annee > 0"
                >
                  mais vous n'étiez pas encore né
                </p>
              </div>
              <p class="histoire__txt">{{ event.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!--Films sortis-->
  <div v-if="movies && cinemaBool" class="movies">
    <h1 class="movies__ctnTitle">Films sortis cette année</h1>
    <p class="movies__ctnSubtitle">Faites défilez horizontalement</p>
    <div class="scroll__container">
      <div v-for="movie in movies" :key="movie.id" class="scroll__item">
        <div
          style="display: flex; justify-content: flex-end; position: relative"
        >
          <svg
            style="position: absolute; top: 50%; transform: translateY(-50%)"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 1380.5 144.22"
          >
            <path
              class="cls-1"
              d="M12.52,80.1c25.87-30.14,61.5-49.9,100.86-55.58,43.34-6.25,83.95,6.07,121.81,26.54,41.54,22.46,82.35,45.53,126.45,62.79,43.77,17.14,90.04,28.85,137.19,30.22,98.6,2.86,191.3-38.75,283.79-66.94,49.28-15.02,99.12-28.11,149-41.01,48.38-12.51,99.32-28.06,149.71-19.1,44.81,7.96,84.41,31.58,125.39,50.02,20.67,9.3,41.68,17.43,64.13,21.19,23.15,3.88,46.62,4.08,69.87.93,11.67-1.58,23.16-3.99,34.49-7.15,9.28-2.59,5.34-17.07-3.99-14.46-46.7,13.03-95.3,11.62-140.45-6.42-41.86-16.73-80.59-41.04-124.13-53.58-48.64-14.01-97.53-6.44-145.72,5.56s-99.67,25.51-149.08,39.72c-48.64,13.99-96.3,30.77-144.52,46.08-46.55,14.78-94.33,27.63-143.34,29.92-97.88,4.58-187.07-38.24-270.38-84.75-20.25-11.3-40.96-22.19-63.33-28.67-19.01-5.51-39.04-8.1-58.82-7.44-39.45,1.31-77.64,15.37-108.17,40.44-7.76,6.37-14.85,13.45-21.39,21.07s4.31,17.95,10.61,10.61h0Z"
              :fill="secondaryColor"
            />
          </svg>
          <fleur_semieronde
            class="movies__flower"
            id="2"
            :couleur="secondaryColor"
            style="width: 300px; height: 300px"
          />
        </div>
        <div class="movies__content">
          <div>
            <a
              :href="
                'https://www.google.com/search?q=' +
                encodeURIComponent(movie.title)
              "
              target="_blank"
            >
              <p class="movies__title">
                {{ movie.title }}
              </p>
            </a>
            <p class="movies__date">
              <span style="font-weight: 800">Date de sortie</span> :
              {{ movie.release_date }}
            </p>
            <p class="movies__description">{{ movie.overview }}</p>
          </div>
          <img
            class="movies__image"
            v-if="getImageUrl(movie.poster_path)"
            :src="getImageUrl(movie.poster_path)"
            alt="Movie Poster"
            style="width: 60%; height: 60%"
          />
          <MoviesDB class="movies__logo" />
        </div>
      </div>
    </div>
  </div>

  <!--Calculateur d'âge-->
  <c-age
    :year="yearFromURL"
    :month="monthFromURL_before"
    :day="dayFromURL"
    :couleur="secondaryColor"
    class="e-id__age"
  />

  <!-- Template HTML -->
  <div class="share">
    <p class="share__txt">
      Partagez votre jour avec vos amis. Copiez le lien et partagez le où vous
      voulez.
    </p>
    <button class="share__btn" @click="copyPageUrl">Copier le lien</button>
    <!-- Ajoutez d'autres boutons pour le partage sur les réseaux sociaux si nécessaire -->
  </div>

  <!--Fenetre des filtres-->
  <div
    class="invisible"
    :class="{
      efilter: isFilterOpen(),
      visible: isFilterOpen(),
      animation: isFilterOpen(),
      //inverse: !isFilterOpen(),
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
    <p class="efilter__text">Choisissez une catégorie d’évènement</p>
    <div class="efilter__Blockflowers">
      <fleur_semieronde2
        id="5"
        @click="inverserCardOpen(1)"
        class="efilter__flowers"
        :couleur="secondaryColor"
      />
      <fleur_pointue
        id="6"
        @click="inverserCardOpen(2)"
        class="efilter__flowers"
        :couleur="secondaryColor"
      />
    </div>
    <div class="efilter__Blockflowers">
      <fleur_semieronde
        id="7"
        @click="inverserCardOpen(3)"
        class="efilter__flowers"
        :couleur="secondaryColor"
      />
    </div>
  </div>

  <c-card_filter
    v-if="FilterChoice == 'naza' && card_open"
    :couleur="secondaryColor"
    :couleur2="primaryColor"
    title="Photo du jour"
    text="Chaque jour, la Naza prend une photo de l'univers. Découvrez celle qui a été prise le jour de votre naissance."
    fleur="semieronde2"
    filterChoice="naza"
    class="efilter__card"
  />
  <c-card_filter
    v-else-if="FilterChoice == 'histoire' && card_open"
    :couleur="secondaryColor"
    :couleur2="primaryColor"
    title="Evénements historiques"
    text="Découvrez tout les évènements historiques qui sont arrivés à chacun de vos anniversaire !"
    fleur="pointue"
    filterChoice="story"
    class="efilter__card"
  />
  <c-card_filter
    v-else-if="FilterChoice == 'cinema' && card_open"
    :couleur="secondaryColor"
    :couleur2="primaryColor"
    title="Sorties cinéma"
    text="Pour chacun de vos anniversaires découvrez les sorties cinéma du jour."
    fleur="semieronde"
    filterChoice="cinema"
    class="efilter__card"
  />

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
    gap: rem(33);
    display: none;
    @include medium-up {
      display: flex;
      margin-top: rem(10);
    }
    @include large-up {
      margin-top: rem(40);
    }
    @include x-large-up {
      margin-top: rem(60);
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

.invisible {
  display: none;
}
.efilter {
  display: block;
  position: fixed;
  z-index: 10;
  background-color: v-bind(primaryColor);
  width: 100%;
  height: 100vh;

  @include medium-up {
    display: none;
  }

  &__card {
    @include medium-up {
      display: none;
    }
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

// Fenetre qui s'en va avec animation
/*.inverse {
  animation: retour 2s forwards;
}

@keyframes retour {
  from {
    transform: translateY(-100%);
  }
  to {
    transform: translateY(0);
  }
}*/

.APOD {
  margin: rem(50) rem(20);
  font-family: Urbanist;
  font-weight: 600;

  @include large-up {
    display: flex;
    flex-direction: column;
    text-align: left;
    align-items: center;
    margin: rem(100) rem(50);
  }

  @include x-large-up {
    display: flex;
    flex-direction: row;
    gap: rem(40);
    text-align: left;
    margin: rem(100) rem(50);
  }

  &__title {
    font-size: $big-font-size;
    color: v-bind(secondaryColor);
    margin-bottom: rem(20);
    text-transform: uppercase;
    font-family: BrownSugar;
    text-align: center;

    @include medium-up {
      text-align: left;
    }
  }

  &__name {
    font-size: $medium-font-size;
    color: v-bind(secondaryColor);
    margin-bottom: rem(20);
    text-decoration: underline;
  }

  &__txt {
    font-size: $regular-font-size;
    color: v-bind(secondaryColor);
    margin-bottom: rem(20);
    line-height: 1.4;
    font-weight: 700;
  }

  &__img {
    width: 100%;
    height: auto;

    @include large-up {
      width: 60%;
    }
    @include x-large-up {
      max-width: 50%;
    }
  }
}

.movies {
  margin: rem(100) rem(20);

  font-family: Urbanist;
  font-weight: 600;

  &__ctnTitle {
    font-family: BrownSugar;
    font-size: $big-font-size;
    color: v-bind(secondaryColor);
    text-transform: uppercase;
    text-align: center;
    margin-bottom: rem(50);

    @include medium-up {
      font-size: $bigger-font-size;
    }

    @include large-up {
      font-size: $giant-font-size;
    }
  }

  &__ctnSubtitle {
    font-family: Urbanist;
    font-size: $regular-font-size;
    color: v-bind(secondaryColor);
    text-transform: uppercase;
    font-style: italic;
    text-align: center;
    margin-bottom: rem(50);
  }

  &__content {
    padding: rem(20);
    border: 2px solid v-bind(secondaryColor);
    border-bottom-left-radius: rem(20);
    border-bottom-right-radius: rem(20);
    margin: 20px;
    margin-top: rem(-150);
    background-color: v-bind(primaryColor);
    z-index: 4;
  }

  &__title {
    font-size: $big-font-size;
    color: v-bind(secondaryColor);
    margin-bottom: rem(20);
    text-decoration: underline;
    margin-top: rem(100);
  }

  &__description {
    font-size: $regular-font-size;
    color: v-bind(secondaryColor);
    margin-bottom: rem(20);
    line-height: 1.4;
    font-weight: 700;
  }

  &__date {
    font-size: $regular-font-size;
    color: v-bind(secondaryColor);
    margin-bottom: rem(20);
    line-height: 1.4;
    font-weight: 900;
  }

  &__logo {
    margin: rem(0) rem(20);
    width: 20%;
  }
}
.scroll__container {
  display: flex;
  overflow-x: auto; /* Permet le défilement horizontal */
}
.scroll__item {
  flex: 0 0 auto; /* Les éléments enfants ne grandissent pas, ne rétrécissent pas, mais sont basés sur leur taille automatique */
  width: clamp(300px, 100%, 600px); /* ou toute autre largeur fixe */
}

.histoire {
  margin: rem(100) rem(20);
  color: v-bind(secondaryColor);
  font-family: Urbanist;
  font-weight: 600;

  &__ctnTitle {
    font-family: BrownSugar;
    font-size: $big-font-size;
    text-transform: uppercase;
    text-align: center;
    margin-bottom: rem(50);

    @include medium-up {
      font-size: $bigger-font-size;
    }

    @include large-up {
      font-size: $giant-font-size;
    }
  }

  &__ctnSubtitle {
    font-family: Urbanist;
    font-size: $regular-font-size;
    color: v-bind(secondaryColor);
    text-transform: uppercase;
    font-style: italic;
    text-align: center;
    margin-bottom: rem(50);

    &.--title {
      display: none;
      @include medium-up {
        display: block;
      }
    }
  }

  &__subText {
    font-family: Urbanist;
    font-size: $medium-font-size;
    color: v-bind(secondaryColor);
    font-style: italic;
    margin-top: rem(150);
    font-weight: 700;

    &--1 {
      margin-bottom: 0;
    }

    &--2 {
      margin-top: 0;
    }

    &--3 {
      margin-top: 0;
    }
  }

  &__txt {
    font-family: Urbanist;
    font-size: $big-font-size;
    color: v-bind(secondaryColor);
    font-weight: 700;
  }

  &__content {
    padding: rem(20);
    border: 2px solid v-bind(secondaryColor);
    border-bottom-left-radius: rem(20);
    border-bottom-right-radius: rem(20);
    margin: 20px;
    margin-top: rem(-150);
    background-color: v-bind(primaryColor);
    z-index: 4;
  }
}

/* Style CSS */
.share {
  margin: rem(-50) rem(20) rem(0) rem(20);
  text-align: center;
  margin-top: 20px;

  &__txt {
    font-family: Urbanist;
    font-size: $regular-font-size;
    color: v-bind(secondaryColor);
    text-transform: uppercase;
    font-style: italic;
    text-align: center;
  }

  &__btn {
    font-family: Urbanist;
    font-size: $regular-font-size;
    color: v-bind(primaryColor);
    text-transform: uppercase;
    text-align: center;
    margin-bottom: rem(50);
    background-color: v-bind(secondaryColor);
    border: none;
    border-radius: 5px;
    padding: 10px;
    cursor: pointer;
  }
}

a {
  text-decoration: none;
}
</style>
