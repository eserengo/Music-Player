<script>
export default {
  name: "nextIcon",
}
</script>

<template>
  <svg
    width="32" 
    height="32" 
    viewBox="0 0 32 32" 
    fill="none" 
    xmlns="http://www.w3.org/2000/svg" 
    title="next track"
    role="img"
    tabindex="0" 
    class="next"
  >
    <path d="M14.1864 14.2517L8.30466 10.9841C6.9716 10.2435 5.33337 11.2074 5.33337 12.7324V19.2676C5.33337 20.7926 6.9716 21.7566 8.30466 21.016L14.1864 17.7483C15.558 16.9863 15.558 15.0137 14.1864 14.2517Z" fill=""/>
    <path d="M21.3334 22.6667L21.3334 9.33335" stroke="" stroke-width="2" stroke-linecap="round"/>
    <path d="M26.6667 22.6667L26.6667 9.33335" stroke="" stroke-width="2" stroke-linecap="round"/>
  </svg>
</template>

<style scoped lang="scss">
@import "../../styles/colorPalette.scss";

.next {
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
