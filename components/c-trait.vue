<script setup>
defineProps({
  couleur: String,
  day: Number,
  month: String,
  year: Number,
});

const dayFromURL = ref(null);
</script>

<template>
  <div class="component">
    <div>
      <div class="e-component__box"></div>
      <div class="e-component__box"></div>
    </div>
    <div class="e-component__point"></div>
    <div class="e-component__para">
      <div class="e-component__text --little">{{ day }} {{ month }}</div>
      <div class="e-component__text --big">{{ year }}</div>
    </div>
    <div class="e-component__point"></div>
    <div>
      <div class="e-component__box"></div>
      <div class="e-component__box"></div>
    </div>
  </div>
</template>

<script setup></script>

<style lang="scss" scoped>
.component {
  display: flex;
  gap: rem(35);
  align-items: center;
}
.e-component {
  &__text {
    color: v-bind(couleur);
    font-family: $secondary-font-family;

    &.--little {
      @include only-small {
        font-size: $medium-font-size;
      }
      font-size: $bigger-font-size;
    }

    &.--big {
      font-size: $giant-font-size;
    }
  }

  &__box {
    border: solid;
    border-bottom: rem(0.1);
    border-color: v-bind(couleur);
    width: 20px;
    @include medium-up {
      width: 100px;
    }
    @include large-up {
      width: 200px;
    }
  }

  &__para {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  &__point {
    width: rem(10);
    height: rem(10);
    background: v-bind(couleur);
    border-radius: 9999px;
  }
}
</style>
