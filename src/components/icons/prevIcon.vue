<script>
export default {
  name: "prevIcon",
}
</script>

<template>
  <svg
    width="32" 
    height="32" 
    viewBox="0 0 32 32" 
    fill="none" 
    xmlns="http://www.w3.org/2000/svg" 
    title="prev track"
    role="img"
    tabindex="0" 
    class="prev"
  >
    <path d="M17.8136 14.2517L23.6953 10.9841C25.0284 10.2435 26.6666 11.2074 26.6666 12.7324V19.2676C26.6666 20.7926 25.0284 21.7566 23.6953 21.016L17.8136 17.7483C16.442 16.9863 16.442 15.0137 17.8136 14.2517Z" fill=""/>
    <path d="M10.6666 22.6667L10.6666 9.33335" stroke="" stroke-width="2" stroke-linecap="round"/>
    <path d="M5.33325 22.6667L5.33325 9.33335" stroke="" stroke-width="2" stroke-linecap="round"/>
  </svg>
</template>

<style scoped lang="scss">
@import "../../styles/colorPalette.scss";

.prev {
  & path {
    fill: $clr-dark-gray;
    stroke: $clr-dark-gray;
  }

  &:hover,
  &:focus {
    cursor: pointer;
    & path {
      fill: $clr-light-gray;
      stroke: $clr-light-gray;
    }
  }
}
</style>
