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
      fill-rule="evenodd"
      clip-rule="evenodd"
      d="M40.1697 0.831154C39.0623 -0.27705 37.2668 -0.277052 36.1595 0.831152L20.4512 16.5511L4.84074 0.929103C3.73335 -0.179101 1.93793 -0.1791 0.83054 0.929103C-0.276845 2.03731 -0.276847 3.83406 0.830538 4.94226L16.441 20.5642L0.958812 36.0578C-0.148573 37.166 -0.148573 38.9627 0.958813 40.071C2.0662 41.1792 3.86162 41.1792 4.96901 40.071L20.4512 24.5774L36.0312 40.1689C37.1386 41.2771 38.934 41.2771 40.0414 40.1689C41.1488 39.0607 41.1488 37.2639 40.0414 36.1557L24.4614 20.5642L40.1697 4.84431C41.277 3.73611 41.277 1.93936 40.1697 0.831154Z"
      :fill="couleur"
    ></path>
  </svg>
</template>
