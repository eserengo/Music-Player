<script>
import { ref } from "vue"
import tracksList from "./tracksList.json"
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
      timer: null,
      art: {
        type: String,
        default: null,
      },
      title: {
        type: String,
        default: null,
      },
      artist: {
        type: String,
        default: null,
      },
      currentTime: {
        type: String,
        default: "00:00",
      },
      totalDuration: {
        type: String,
        default: "00:00",
      },
      slider: {
        type: Number,
        default: 0,
      }
    }
  },
  setup() {
    const index = ref(0);
    const isPlaying = ref(false);

    const toggleIsPlaying = () => {
      isPlaying.value = !isPlaying.value;
    }

    return {
      index,
      isPlaying,
      toggleIsPlaying,
    }
  },
  methods: {
    // Function to reset all values to their default
    resetValues() {
      this.currentTime = "00:00";
      this.totalDuration = "00:00";
      this.slider = 0;
    },
    
    loadTrack(tracksIndex) {
      const target = tracksList[tracksIndex];
      // Clear the previous seek timer
      clearInterval(this.timer);
      this.resetValues();
    
      // Load a new track
      this.$refs.track.src = target.source;
      this.$refs.track.load();
    
      // Update details of the track
      this.art = target.art;
      this.title = target.title;
      this.artist = target.artist;

      //Update track ranges
      this.totalDuration = this.$refs.track.duration;
      this.currentTime = this.$refs.track.currentTime;
    
      // Set an interval of 1000 milliseconds
      // for updating the seek slider
      this.timer = setInterval(this.seekUpdate, 1000);
    
      // Move to the next track if the current finishes playing
      // using the 'ended' event
      this.$refs.track.addEventListener("ended", this.nextTrack);
    },

    playTrack() {
      // Play the loaded track
      this.$refs.track.play();
      !this.isPlaying && this.toggleIsPlaying();
    },

    pauseTrack() {
      // Pause the loaded track
      this.$refs.track.pause();
      this.isPlaying && this.toggleIsPlaying();
    },

    nextTrack() {
      // Go back to the first track if the
      // current one is the last in the track list
      (this.index < tracksList.length - 1) ? this.index++ : this.index = 0;
    
      // Load and play the new track
      this.loadTrack(this.index);
      this.isPlaying && this.playTrack();
    },

    prevTrack() {
      // Go back to the last track if the
      // current one is the first in the track list
      (this.index > 0) ? this.index-- : this.index = tracksList.length - 1;
      
      // Load and play the new track
      this.loadTrack(this.index);
      this.isPlaying && this.playTrack();
    },

    seekUpdate() {    
      // Check if the current track duration is a legible number
      if (!isNaN(this.$refs.track.duration)) {
        const seekPosition = (this.$refs.track.currentTime / this.$refs.track.duration) * 100;
        this.slider = seekPosition;

        // Calculate the time left and the total duration
        const currentMinutes = Math.floor(this.$refs.track.currentTime / 60);
        const currentSeconds = Math.floor(this.$refs.track.currentTime % 60);
        const durationMinutes = Math.floor(this.$refs.track.duration / 60);
        const durationSeconds = Math.floor(this.$refs.track.duration % 60);

        // Display the updated duration
        this.currentTime = `${currentMinutes}:${currentSeconds < 10 ? '0' : ''}${currentSeconds}`;
        this.totalDuration = `${durationMinutes}:${durationSeconds < 10 ? '0' : ''}${durationSeconds}`;
      }
    },

    handleSliderChange() {
      // Calculate the new currentTime based on the slider value
      const newTime = (this.slider / 100) * this.$refs.track.duration;
      
      // Update the audio's currentTime
      this.$refs.track.currentTime = newTime;
      
      // Update the displayed time
      this.seekUpdate();
    },
  },
  mounted() {
    this.loadTrack(this.index);
  },
}
</script>

<template>
  <div class="music-app">
    <main class="player">

      <audio ref="track"></audio>

      <article class="details">
        <section class="art" :style="{ 'backgroundImage': `url('${art}')` }"></section>
        <section class="title" v-text="title"></section>
        <section class="artist" v-text="artist"></section>
      </article>

      <article class="track-range">
        <section class="current" v-text="currentTime"></section>
        <input 
          type="range" 
          min="0" 
          max="100"
          tabindex="0"
          class="slider"
          v-model="slider"
          @input="handleSliderChange"
        >
        <section class="total" v-text="totalDuration"></section>
      </article>

      <article class="controls">
        <prevIcon @click="prevTrack" />
        <component
          :is="!isPlaying ? 'playIcon' : 'pauseIcon'"
          @click="!this.isPlaying ? this.playTrack() : this.pauseTrack()"
          class="btn"
        />
        <nextIcon @click="nextTrack" />
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
  padding: min(5vw, 1rem);
  display: flex;
  flex-flow: column nowrap;
  align-items: center;
  justify-content: center;

  .player {  
  background-color: $clr-opaque;  
  display: flex;
  flex-flow: column nowrap;
  align-items: center;
  gap: 1rem;
  padding: 1rem;
  border-radius: 1rem;
  border: 1px solid $clr-opaque;
  box-shadow: $shadow;

    .details {
      display: flex;
      flex-flow: column nowrap;
      align-items: center;

      .art {
        width: 996px;
        aspect-ratio: 3;
        border-radius: 0.75rem;
        box-shadow: $shadow;
        background-position: top left;
        background-size: cover;
        background-repeat: no-repeat;
        background-image: url("./assets/faelands_8.jpg");
      }

      .title {
        color: $clr-light-gray;
        font-size: min(8vw, 1.25rem);
        font-size: max(1rem, min(8vw, 1.25rem));
        font-weight: 400;
        text-align: center;
        margin-block: 1rem 0.5rem;
      }

      .artist {
        color: $clr-dark-gray;
        font-size: min(5vw, 0.75rem);
        font-size: max(0.75rem, min(5vw, 0.75rem));
        text-align: center;
      }
    }

    .track-range {
      position: relative;
      width: 100%;

      .current,
      .total {
        position: absolute;
        top: 0;
        color: $clr-dark-gray;
        font-size: 0.75rem;
      }

      .current {
        left: 0;
      }

      .total {
        right: 0;
      }

      .slider {
        accent-color: $clr-pink;
        background-color: $clr-light-gray;
        width: 100%;
        margin-top: 1.5rem;
        
        &::-webkit-slider-thumb {
          cursor: ew-resize;
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
