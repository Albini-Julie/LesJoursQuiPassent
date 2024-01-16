<template>
  <div class="e-mentions">
    <div class="e-mentions__header">
      <croix @click="retourPagePrecedente" :couleur="secondaryColor" />
    </div>

    <div class="e-mentions__Blocktitle">
      <h2 class="e-mentions__title">Mentions légales</h2>
    </div>

    <div class="e-mentions__littleFlower">
      <FleurSemieronde :couleur="secondaryColor" />
      <FleurRonde :couleur="secondaryColor" />
    </div>

    <div class="e-mentions__content">
      <GiantFlower2 class="e-mentions__flower --2" :couleur="secondaryColor" />
      <div class="e-mentions__Blocktext">
        <p class="e-mentions__Contenttext" style="text-decoration: underline">
          Projet "Les Jours Qui Passent" du département MMI de Montbéliard
        </p>
        <br />
        <p class="e-mentions__Contenttext">
          4 Pl. Lucien Tharradin, 25200 Montbéliard - Département MMI Montbéliard
        </p>
        <p class="e-mentions__Contenttext">lesjoursquipassent@gmail.com</p>
        <p class="e-mentions__Contenttext">07 60 38 72 51</p>
        <br />
        <p class="e-mentions__Contenttext" style="text-decoration: underline">
          Responsable de la Publication :
        </p>
        <br />
        <p class="e-mentions__Contenttext">
          Lilian Chesneau-Ciccarelli et Julie Albini, partie développement du projet.
        </p>
        <br />
        <p class="e-mentions__Contenttext" style="text-decoration: underline">
          Hébergement du Site :
        </p>
        <br />
        <p>Vercel</p>
        <br />
        <p class="e-mentions__Contenttext" style="text-decoration: underline">
          Propriété Intellectuelle :
        </p>
        <br />
        <p class="e-mentions__Contenttext">
          L’ensemble du contenu de ce site web, y compris les textes, les graphiques, les logos, les
          images, les clips audio et vidéo, est la propriété du département MMI Montbéliard et est
          protégé par les lois sur la propriété intellectuelle. Toute reproduction, distribution, ou
          utilisation non autorisée de ce contenu est strictement interdite.
        </p>
      </div>
    </div>

    <div class="e-mentions__content --2">
      <div class="e-mentions__Blocktext --2">
        <p class="e-mentions__Contenttext --top" style="text-decoration: underline">
          Collecte et Utilisation des Données Personnelles :
        </p>
        <br />
        <p class="e-mentions__Contenttext">
          Veuillez vous référer à notre politique de confidentialité pour des informations
          détaillées sur la collecte et l’utilisation des données personnelles.
        </p>
        <br />
        <p class="e-mentions__Contenttext" style="text-decoration: underline">Liens Externes :</p>
        <br />
        <p class="e-mentions__Contenttext --top">
          Ce site web peut contenir des liens vers des sites tiers. Les jours qui passent n’assume
          aucune responsabilité quant au contenu ou aux pratiques de confidentialité de ces sites
          tiers.
        </p>
        <br />
        <p class="e-mentions__Contenttext --top" style="text-decoration: underline">
          Responsabilité :
        </p>
        <br />
        <p class="e-mentions__Contenttext">
          <br />
          Bien que nous nous efforçons de fournir des informations précises et à jour, Les jours qui
          passent ne garantit pas l’exactitude ni l’exhaustivité du contenu de ce site web. Les
          jours qui passent décline toute responsabilité pour tout dommage résultant de
          l’utilisation de ce site web.
        </p>
        <p class="e-mentions__Contenttext --top" style="text-decoration: underline">
          Modification des Mentions Légales :
        </p>
        <p class="e-mentions__Contenttext --top">
          Les jours qui passent se réserve le droit de modifier ces mentions légales à tout moment.
          Les utilisateurs sont encouragés à consulter régulièrement cette page pour rester informés
          des mises à jour.
        </p>
        <p class="e-mentions__Contenttext --top" style="text-decoration: underline">Contact :</p>
        <br />
        <p class="e-mentions__Contenttext" style="margin-bottom: 100px">
          Pour toute question ou demande de renseignements concernant ces mentions légales, veuillez
          nous contacter à lesjoursquipassentcontact@gmail.com.
        </p>
      </div>
      <GiantFlower class="e-mentions__flower" :couleur="secondaryColor" />
    </div>
    <div class="e-mentions__littleFlower">
      <FleurSemieronde2 :couleur="secondaryColor" />
      <FleurPointue :couleur="secondaryColor" />
    </div>
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted } from "vue";
import { useRouter } from "vue-router";

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
.e-mentions {
  &__Blocktitle {
    font-family: $primary-font-family;
    font-size: $big-font-size;
    color: v-bind(secondaryColor);
    display: flex;
    justify-content: center;
    text-align: center;
    @include medium-up {
      font-size: $bigger-font-size;
    }
    @include large-up {
      font-size: $giant-font-size;
    }
  }

  &__title {
    margin-bottom: 0px;
    @include large-up {
      margin-bottom: rem(40);
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
      margin: rem(0);
    }
    @include large-up {
      width: 50%;
    }
    @include x-large-up {
    }
  }

  &__content {
    display: block;
    @include large-up {
      display: flex;
      justify-content: space-between;
      margin-top: rem(50);
    }

    &.--2 {
      align-items: center;
    }
  }

  &__footer {
    @include medium-up {
      margin-top: rem(70);
    }
    @include x-large-up {
      margin-top: rem(80);
    }
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

  &__Blocktext {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    font-family: $primary-font-family;
    font-size: $regular-font-size;
    color: v-bind(secondaryColor);
    margin-right: rem(20);
    margin-left: rem(20);
    @include large-up {
      margin-right: rem(100);
      margin-left: rem(0);
      width: 55%;
    }
    @include x-large-up {
      margin-right: rem(200);
      margin-left: rem(0);
    }

    &.--2 {
      @include large-up {
        margin-left: rem(100);
        margin-top: rem(40);
      }
      @include x-large-up {
        margin-left: rem(200);
        margin-top: rem(0);
      }
    }
  }

  &__Contenttext {
    margin: 0px;

    &.--top {
      margin-top: rem(20);
    }
  }

  &__flower {
    display: none;
    @include large-up {
      display: block;
      width: 30%;
      height: 30%;
    }
    &.--2 {
      width: 20%;
      height: 20%;
      @include large-up {
        width: 20%;
        height: 20%;
      }
    }
  }

  &__littleFlower {
    display: flex;
    justify-content: center;
    margin-top: rem(50);
    margin-bottom: rem(50);
    gap: rem(10);
    @include large-up {
      display: none;
    }
  }
}
</style>
