<script>
export default {
  name: "pauseIcon",
}
</script>

<template>
  <svg 
    width="32px" 
    height="32px" 
    viewBox="-14 -14 84 84" 
    xmlns="http://www.w3.org/2000/svg" 
    title="pause track"
    role="img"
    tabindex="0" 
    class="pause"
  >
    <path d="M 20.2656 47.3594 C 21.3672 47.3594 22.2578 46.5156 22.2578 45.4141 L 22.2578 10.6094 C 22.2578 9.5078 21.3672 8.6406 20.2656 8.6406 C 19.1641 8.6406 18.25 9.5078 18.25 10.6094 L 18.25 45.4141 C 18.25 46.5156 19.1641 47.3594 20.2656 47.3594 Z M 35.7578 47.3594 C 36.8594 47.3594 37.75 46.5156 37.75 45.4141 L 37.75 10.6094 C 37.75 9.5078 36.8594 8.6406 35.7578 8.6406 C 34.6563 8.6406 33.7422 9.5078 33.7422 10.6094 L 33.7422 45.4141 C 33.7422 46.5156 34.6563 47.3594 35.7578 47.3594 Z"/>
  </svg>
</template>

<style scoped lang="scss">
@import "../../styles/colorPalette.scss";

.pause {
  & path {
    fill: $clr-light-gray;
  }

  &:hover,
  &:focus {
    cursor: pointer;
  }
}
</style>
