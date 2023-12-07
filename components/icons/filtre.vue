<script setup>
defineProps({
  couleur: String,
});
</script>

<template>
  <svg
    width="41"
    height="41"
    viewBox="0 0 41 41"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
    style="width: 41px; height: 41px"
    preserveAspectRatio="none"
  >
    <path
      d="M39 4C24.2319 6.74549 16.1053 6.93639 2 4C2 4 15.627 13.5244 16.8 21.3433C17.973 29.1623 16.8 33.3333 16.8 33.3333L24.2 37C24.2 37 21.4023 30.2354 24.2 21.3433C26.9977 12.4512 39 4 39 4Z"
      :stroke="couleur"
      stroke-width="3.41667"
      stroke-linecap="round"
      stroke-linejoin="round"
    ></path>
  </svg>
</template>
