<script setup>
defineProps({
  couleur: String,
});
</script>

<template>
  <svg
    width="31"
    height="60"
    viewBox="0 0 31 60"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
    style="width: 30.82px; height: 60px"
    preserveAspectRatio="xMidYMid meet"
  >
    <g clip-path="url(#clip0_333_7143)">
      <path
        d="M6.98598 10.6812H6.90761C6.53896 21.3392 6.94679 29.6439 0 29.6439C6.94679 29.6439 6.53896 37.9485 6.90761 48.6066H6.98598C7.35463 37.9485 6.94679 29.6439 13.8936 29.6439C6.94679 29.6439 7.35383 21.3392 6.98598 10.6812Z"
        :fill="couleur"
      ></path>
    </g>
    <g clip-path="url(#clip1_333_7143)">
      <path
        d="M16.7926 0H16.7142C16.3456 10.6581 16.7534 18.9627 9.80664 18.9627C16.7534 18.9627 16.3456 27.2674 16.7142 37.9255H16.7926C17.1613 27.2674 16.7534 18.9627 23.7002 18.9627C16.7534 18.9627 17.1605 10.6581 16.7926 0Z"
        :fill="couleur"
      ></path>
    </g>
    <g clip-path="url(#clip2_333_7143)">
      <path
        d="M23.9127 22.0747H23.8344C23.4657 32.7328 23.8736 41.0374 16.9268 41.0374C23.8736 41.0374 23.4657 49.3421 23.8344 60.0002H23.9127C24.2814 49.3421 23.8736 41.0374 30.8203 41.0374C23.8736 41.0374 24.2806 32.7328 23.9127 22.0747Z"
        :fill="couleur"
      ></path>
    </g>
    <defs>
      <clipPath id="clip0_333_7143">
        <rect
          width="13.8936"
          height="37.9255"
          fill="white"
          transform="translate(0 10.6812)"
        ></rect>
      </clipPath>
      <clipPath id="clip1_333_7143">
        <rect
          width="13.8936"
          height="37.9255"
          fill="white"
          transform="translate(9.80664)"
        ></rect>
      </clipPath>
      <clipPath id="clip2_333_7143">
        <rect
          width="13.8936"
          height="37.9255"
          fill="white"
          transform="translate(16.9268 22.0747)"
        ></rect>
      </clipPath>
    </defs>
  </svg>
</template>
