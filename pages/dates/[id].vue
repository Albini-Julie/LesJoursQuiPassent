<script>
import axios from "axios";

export default {
  data() {
    return {
      apodData: null,
      dateFromURL: null,
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

    // Appeler la méthode fetchApod après avoir récupéré la date
    this.fetchApod();
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
  created() {
    // Notez que la méthode fetchApod est maintenant appelée dans mounted
    // après avoir récupéré la date de l'URL
  },
};
</script>

<template>
  <div v-if="apodData">
    <h3>{{ apodData.title }}</h3>
    <p>{{ apodData.explanation }}</p>
    <img :src="apodData.url" alt="NASA APOD" />
  </div>
</template>
