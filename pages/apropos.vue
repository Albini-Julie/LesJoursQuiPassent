<template>
  <div class="e-propos">
    <div class="e-propos__header">
      <croix @click="retourPagePrecedente" :couleur="secondaryColor" />
    </div>
    <!--Title-->
    <div class="e-propos__title">
      <h2>À propos</h2>
    </div>
    <div class="e-propos__content">
      <!--Flower mobile-->
      <div class="e-propos__blockFlower">
        <GiantFlower class="e-propos__flower --mobile" :couleur="secondaryColor" />
      </div>
      <!--Text-->
      <p class="e-propos__text">
        Le projet « Les Jours qui Passent » se concentre sur une fusion harmonieuse entre la
        technologie moderne et la poésie intemporelle de la condition humaine. Il s’agit d’un
        service web innovant qui permet à l’utilisateur de se connecter avec sa propre histoire en
        lui offrant la possibilité d’explorer le temps qu’il a passé sur cette Terre jusqu’à ce
        moment précis. Ce voyage dans le temps personnel est accompagné d’informations riches et
        fascinantes sur son jour de naissance et les événements marquants qui ont façonné le monde
        au fil des années qu’il a vécues sur cette Terre. Venez découvrir les merveilles de ce
        projet et comment il peut transformer une simple date de naissance en une expérience
        profondément poétique et enrichissante.
      </p>
      <!--Flower desktop-->
      <GiantFlower class="e-propos__flower" :couleur="secondaryColor" />
    </div>
    <!--Footer-->
    <c-footer class="e-propos__footer" :couleur="secondaryColor" />
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted } from "vue";
import { useRoute, useRouter } from "vue-router";

export default {
  setup() {
    const primaryColor = ref("");
    const secondaryColor = ref("");
    const router = useRouter();

    const setColor = () => {
      const date = new Date();
      const day = date.getDate();
      const month = date.getMonth() + 1;

      if ((month === 12 && day >= 21) || month === 1 || month === 2 || (month === 3 && day < 21)) {
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

    const retourPagePrecedente = () => {
      router.go(-1);
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
      retourPagePrecedente,
    };
  },
};
</script>

<style lang="scss" scoped>
.e-propos {
  &__title {
    font-family: $primary-font-family;
    font-size: $bigger-font-size;
    color: v-bind(secondaryColor);
    display: flex;
    justify-content: center;
    @include medium-up {
      font-size: $giant-font-size;
    }
    @include large-up {
      font-size: $giant-font-size;
    }
  }

  &__text {
    font-family: $primary-font-family;
    font-size: $regular-font-size;
    color: v-bind(secondaryColor);
    display: flex;
    justify-content: center;
    margin-left: rem(20);
    margin-right: rem(20);
    @include medium-up {
      margin-left: rem(80);
      margin-right: rem(80);
    }
    @include large-up {
      margin-left: rem(40);
      width: 55%;
      margin-right: rem(0);
    }
    @include x-large-up {
      width: 50%;
      margin-left: rem(200);
    }
  }

  &__content {
    display: block;
    @include large-up {
      display: flex;
      justify-content: space-between;
      margin-top: rem(50);
    }
  }

  &__flower {
    display: none;
    @include large-up {
      display: block;
      width: 30%;
      height: 30%;
    }
    @include x-large-up {
      width: auto;
      height: auto;
    }

    &.--mobile {
      display: flex;
      justify-content: flex-end;
      height: 50%;
      width: 50%;
      @include medium-up {
        height: 40%;
        width: 40%;
      }
      @include large-up {
        display: none;
      }
    }
  }

  &__footer {
    margin-top: rem(50);
    @include medium-up {
      margin-top: rem(70);
    }
    @include x-large-up {
      margin-top: rem(20);
    }
  }

  &__blockFlower {
    display: flex;
    justify-content: flex-end;
  }

  &__header {
    margin-right: rem(25);
    margin-top: rem(25);
    display: flex;
    justify-content: flex-end;
    @include medium-up {
      margin-right: rem(50);
      margin-top: rem(50);
    }
  }
}
</style>
