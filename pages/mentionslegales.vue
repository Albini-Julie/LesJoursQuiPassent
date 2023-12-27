<template>
  <div class="e-mentions">
    <div class="e-mentions__header">
      <croix @click="retourPagePrecedente" :couleur="secondaryColor" />
    </div>
    <!--Title-->
    <div class="e-mentions__title">
      <h2>Mentions légales</h2>
    </div>
    <!--Partie 1 (content 1 + fleur 1)-->
    <div class="e-mentions__content">
      <!--Flower desktop-->
      <GiantFlower2 class="e-mentions__flower" :couleur="secondaryColor" />
      <!--Text-->
      <div class="e-mentions__Blocktext">
        <p class="e-mentions__Contenttext">[Adresse de votre site web]</p>
        <p class="e-mentions__Contenttext">
          4 Pl. Lucien Tharradin, 25200 Montbéliard - Département MMI
          Montbéliard
        </p>
        <p class="e-mentions__Contenttext">lesjoursquipassent@gmail.com</p>
        <p class="e-mentions__Contenttext">07 60 38 72 51</p>
        <p class="e-mentions__Contenttext">Responsable de la Publication :</p>
        <p class="e-mentions__Contenttext">
          Lilian Chesneau-Ciccarelli et Julie Albini, partie développement du
          projet
        </p>
        <p class="e-mentions__Contenttext">Hébergement du Site :</p>
        <p class="e-mentions__Contenttext">Infomaniak</p>
        <p class="e-mentions__Contenttext">
          Rue Eugène Marziano 25 - 1227 Les Acacias / Genève
        </p>
        <p class="e-mentions__Contenttext">
          Technoparkstrasse 3 - 8406 Winterthur
        </p>
        <p class="e-mentions__Contenttext">https://www.infomaniak.com/fr</p>
        <p class="e-mentions__Contenttext">Propriété Intellectuelle :</p>
        <p class="e-mentions__Contenttext">
          L’ensemble du contenu de ce site web, y compris les textes, les
          graphiques, les logos, les images, les clips audio et vidéo, est la
          propriété du département MMI Montbéliard et est protégé par les lois
          sur la propriété intellectuelle. Toute reproduction, distribution, ou
          utilisation non autorisée de ce contenu est strictement interdite.
        </p>
      </div>
    </div>

    <!--Partie 2 (Content 2 et fleur 2)-->
    <div class="e-mentions__content">
      <!--Text-->
      <div class="e-mentions__Blocktext --2">
        <p class="e-mentions__Contenttext">
          Collecte et Utilisation des Données Personnelles :
        </p>
        <p class="e-mentions__Contenttext">
          Veuillez vous référer à notre politique de confidentialité pour des
          informations détaillées sur la collecte et l’utilisation des données
          personnelles.
        </p>
        <p class="e-mentions__Contenttext">Liens Externes :</p>
        <p class="e-mentions__Contenttext">
          Ce site web peut contenir des liens vers des sites tiers. Les jours
          qui passent n’assume aucune responsabilité quant au contenu ou aux
          pratiques de confidentialité de ces sites tiers.
        </p>
        <p class="e-mentions__Contenttext">Responsabilité :</p>
        <p class="e-mentions__Contenttext">
          Bien que nous nous efforçons de fournir des informations précises et à
          jour, Les jours qui passent ne garantit pas l’exactitude ni
          l’exhaustivité du contenu de ce site web. Les jours qui passent
          décline toute responsabilité pour tout dommage résultant de
          l’utilisation de ce site web.
        </p>
        <p class="e-mentions__Contenttext">
          Modification des Mentions Légales :
        </p>
        <p class="e-mentions__Contenttext">
          Les jours qui passent se réserve le droit de modifier ces mentions
          légales à tout moment. Les utilisateurs sont encouragés à consulter
          régulièrement cette page pour rester informés des mises à jour.
        </p>
        <p class="e-mentions__Contenttext">Contact :</p>
        <p class="e-mentions__Contenttext">
          Pour toute question ou demande de renseignements concernant ces
          mentions légales, veuillez nous contacter à
          lesjoursquipassentcontact@gmail.com.
        </p>
      </div>
      <!--Flower desktop-->
      <GiantFlower class="e-mentions__flower" :couleur="secondaryColor" />
    </div>

    <!--Footer-->
    <c-footer class="e-mentions__footer" :couleur="secondaryColor" />
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
    @include medium-up {
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
  }

  &__footer {
    margin-top: rem(50);
    @include medium-up {
      margin-top: rem(70);
    }
    @include x-large-up {
      margin-top: rem(80);
    }
  }

  &__blockFlower {
    display: flex;
    justify-content: end;
  }

  &__header {
    margin-right: rem(25);
    margin-top: rem(25);
    display: flex;
    justify-content: end;
    @include medium-up {
      margin-right: rem(50);
      margin-top: rem(50);
    }
  }

  &__Blocktext {
    display: flex;
    flex-direction: column;
    align-items: start;
    font-family: $primary-font-family;
    font-size: $regular-font-size;
    color: v-bind(secondaryColor);
    width: 55%;
    margin-right: rem(200);

    &.--2 {
      margin-left: rem(200);
    }
  }

  &__Contenttext {
    margin: 0px;
  }
}
</style>
