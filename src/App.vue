<script>
import { ref } from "vue"
import prevIcon from "./components/icons/prevIcon.vue"
import nextIcon from "./components/icons/nextIcon.vue"
import playIcon from "./components/icons/playIcon.vue"
import pauseIcon from "./components/icons/pauseIcon.vue"

export default {
  name: "App",
  components: {
    prevIcon,
    nextIcon,
    playIcon,
    pauseIcon,
  },
  data() {
    return {
      currentTrack: document.createElement("audio"),
    }
  },
  setup() {
    const track = ref(0);
    const isPlaying = ref(false);

    const toggleIsPlaying = () => {
      isPlaying.value = !isPlaying.value;
    }

    return {
      track,
      isPlaying,
      toggleIsPlaying,
    }
  },
}
</script>

<template>
  <div class="music-app">
    <main class="player">
      <article class="details">
        <section class="art"><img src="../src/assets/faelands_1.jpg" alt="faelands" /></section>
        <section class="title">Test</section>
        <section class="artist">Test</section>
      </article>

      <article class="track">
        <section class="current">00:00</section>
        <input 
          type="range" 
          min="1" 
          max="100"
          value="0" 
          tabindex="0"
          class="slider"
        >
        <section class="total">00:00</section>
      </article>

      <article class="controls">
        <prevIcon />
        <component
          :is="!isPlaying ? 'playIcon' : 'pauseIcon'"
          @click="toggleIsPlaying"
          class="btn"
        />
        <nextIcon />
      </article>
    </main>
  </div>
</template>

<style lang="scss">
@import "./main.scss";
@import "../src/styles/colorPalette.scss";

.music-app {
  background: url("../src/assets/bg.jpg") no-repeat center;
  background-size: cover;
  min-height: 100vh;
  display: flex;
  flex-flow: column nowrap;
  align-items: center;
  justify-content: center;

  .player {  
  background-color: $clr-opaque;  
  display: flex;
  flex-flow: column nowrap;
  align-items: center;
  gap: 2rem;
  padding: 1rem;
  border-radius: 1rem;
  border: 1px solid $clr-opaque;
  box-shadow: $shadow;
  max-width: 25rem;

    *:hover,
    *:focus {
      outline: none;
    }

    .details {
      display: flex;
      flex-flow: column nowrap;
      align-items: center;

      .art {
        width: 100%;
        aspect-ratio: 3;

        & img {
          border-radius: 0.75rem;
          box-shadow: $shadow;
        }
      }

      .title {
        color: $clr-light-gray;
        font-size: min(8vw, 1.25rem);
        font-weight: 400;
        margin-block: 1rem 0.5rem;
      }

      .artist {
        color: $clr-dark-gray;
        font-size: min(5vw, 0.75rem);
      }
    }

    .track {
      position: relative;
      width: 100%;

      .current {
        position: absolute;
        top: 0;
        left: 0;
        color: $clr-dark-gray;
        font-size: 0.75rem;
      }

      .total {
        position: absolute;
        top: 0;
        right: 0;
        color: $clr-dark-gray;
        font-size: 0.75rem;
      }

      .slider {
        appearance: none;
        width: 100%;
        height: 0.25rem;
        margin-top: 1.5rem;
        background-color: transparent;
        opacity: 0.8;

        &:hover,
        &:focus {
          opacity: 1.0;
          cursor: pointer;
        }

        &::-webkit-slider-thumb {
          -webkit-appearance: none;
          width: 0.5rem;
          aspect-ratio: 1;
          border-radius: 50%;
          background-color: $clr-pink;
          box-shadow: 1px 1px 4px $clr-pink;
        }

        &::-webkit-slider-runnable-track {
          height: 0.5rem;
          background-color: $clr-light-gray;
          box-shadow: $shadow;
          border-radius: 0.5rem;
        }
      }
    }

    .controls {
      display: flex;
      flex-flow: row nowrap;
      align-items: center;
      gap: 1rem;

      .btn {
        width: 2rem;
        aspect-ratio: 1;
        border-radius: 50%;
        background-color: $clr-dark-gray;

        &:hover,
        &:focus {
          background-color: $clr-pink;
          box-shadow: 1px 1px 4px $clr-pink;
        }
      }
    }
  }
}
</style>
