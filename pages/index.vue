<template>
  <!--Vidéo-->
  <div @click="startVideoPlayback" style="position: relative">
    <div ref="videoContainer" class="video-container">
      <video ref="videoRef">
        <source v-if="video == 'winter'" src="/Fleurs_bleues.mp4" type="video/mp4" />
        <source v-else-if="video == 'spring'" src="/Fleurs_roses.mp4" type="video/mp4" />
        <source v-else-if="video == 'summer'" src="/FLEURS_BLANCHES.mp4" type="video/mp4" />
        <source v-else-if="video == 'automn'" src="/Fleurs_marrons.mp4" type="video/mp4" />
      </video>
    </div>
    <p class="absolute">Cliquez ici et défillez vers le bas</p>
  </div>
  <div class="intro">
    <!--Fleur de gauche-->
    <div class="e-intro__fleur">
      <fleur :couleur="secondaryColor" />
    </div>
    <!--Logo-->
    <div class="e-intro">
      <logo class="e-intro__logo" :couleur="secondaryColor" />
      <h2 class="e-intro__title" :style="{ color: secondaryColor }">
        <apostrophe class="e-intro__apo" :couleur="secondaryColor" /> Il est bon de faire confiance
        au temps qui passe : l'avenir nous révèle toujours ses secrets.
        <apostrophe class="e-intro__apo" :couleur="secondaryColor" />
      </h2>
    </div>
    <!--Fleur de droite-->
    <div class="e-intro__fleur --rotate">
      <fleur :couleur="secondaryColor" />
    </div>
  </div>
  <div class="e-intro__button">
    <c-bouton :couleur="secondaryColor" href="/insert">Commencer l'expérience</c-bouton>
  </div>
  <div class="e-intro__button --little">
    <c-bouton size="small" :couleur="secondaryColor" href="/insert"
      >Commencer l'expérience</c-bouton
    >
  </div>
  <div>
    <c-footer class="e-intro__footer" :couleur="secondaryColor" />
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted, defineProps } from "vue";

defineProps({
  primaryColor: String,
  secondaryColor: String,
});

export default {
  props: {
    primaryColor: {
      type: String,
    },
    secondaryColor: {
      type: String,
    },
  },
  setup() {
    const videoContainer = ref(null);
    const videoRef = ref(null);
    let observer;

    const handleIntersection = (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          // L'élément vidéo est visible, ajustez la vitesse de lecture
          videoRef.value.playbackRate = entry.intersectionRatio; // Ajustez la vitesse en fonction de la partie visible
        }
      });
    };

    const startVideoPlayback = () => {
      if (videoRef.value) {
        videoRef.value.play();
      }
    };

    //Fonction pour importer les couleurs selon les saisons
    const primaryColor = ref("");
    const secondaryColor = ref("");
    const video = ref("");

    const setColor = () => {
      const date = new Date();
      const day = date.getDate();
      const month = date.getMonth() + 1;

      if ((month === 12 && day >= 21) || month === 1 || month === 2 || (month === 3 && day < 21)) {
        primaryColor.value = "#FFFFFF";
        secondaryColor.value = "#4359AA";
        video.value = "winter";
      } else if (
        (month === 3 && day >= 21) ||
        month === 4 ||
        (month === 5 && day <= 20) ||
        (month === 6 && day < 21)
      ) {
        primaryColor.value = "#2E3E1A";
        secondaryColor.value = "#D398EF";
        video.value = "spring";
      } else if (
        (month === 6 && day >= 21) ||
        month === 7 ||
        month === 8 ||
        (month === 9 && day < 21)
      ) {
        primaryColor.value = "#D09C14";
        secondaryColor.value = "#FFFFFF";
        video.value = "summer";
      } else if (
        (month === 9 && day >= 21) ||
        month === 10 ||
        month === 11 ||
        (month === 12 && day < 21)
      ) {
        primaryColor.value = "#391B0A";
        secondaryColor.value = "#DE8706";
        video.value = "automn";
      }
    };

    onMounted(() => {
      setColor();
      // Créer un observateur d'intersection
      observer = new IntersectionObserver(handleIntersection, {
        threshold: [0, 0.5, 1],
      });

      onUnmounted(() => {
        setColor();
      });

      // Observer l'élément vidéo
      observer.observe(videoContainer.value);
    });

    return {
      videoContainer,
      videoRef,
      startVideoPlayback,
      primaryColor,
      secondaryColor,
      video,
    };
  },
};

//Fonction pour gérer les couleurs selon les saisons
</script>

<style lang="scss" scoped>
.video-container {
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: black; /* Couleur de fond pendant le défilement */
  overflow: hidden;
}

video {
  @include x-large-up {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
}

.intro {
  display: flex;
  justify-content: space-between;
  padding-top: 115px;
  flex-wrap: wrap;
  @include x-large-up {
    gap: 100px;
    display: flex;
    flex-wrap: nowrap;
  }
}

.e-intro {
  display: flex;
  flex-direction: column;
  align-items: center;

  &__fleur {
    display: none;
    @include large-up {
      display: block;
    }
    @include x-large-up {
      display: block;
    }
    &.--rotate {
      transform: rotate(180deg);
      @include large-up {
        display: none;
      }
      @include x-large-up {
        display: block;
      }
    }
  }

  &__title {
    font-family: $secondary-font-family;
    text-align: center;
    font-size: $big-font-size;
    margin-right: rem(20);
    margin-left: rem(20);
    margin-top: rem(120);
    width: 80%;
    @include medium-up {
      font-size: $bigger-font-size;
    }
    @include large-up {
      font-size: $giant-font-size;
    }
    @include x-large-up {
      font-size: $giant-font-size;
      text-align: start;
      margin-right: 0;
      margin-left: 0;
      width: 100%;
    }
  }

  &__button {
    justify-content: center;
    margin-top: 30px;
    margin-bottom: 80px;
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

  &__apo {
    @include only-small {
      width: rem(30);
      height: rem(30);
    }
  }

  &__logo {
    @include large-up {
      margin-top: rem(50);
    }
  }
}

.absolute {
  position: absolute;
  top: 80%;
  right: 50%;
  transform: translate(50%, -50%);
  font-family: Urbanist;
  font-size: $medium-font-size;
  color: v-bind(secondaryColor);
  font-style: italic;
  font-weight: 700;
  background-color: v-bind(primaryColor);
  padding: rem(5) rem(10);
  border-radius: rem(20);
  text-align: center;
}
</style>
