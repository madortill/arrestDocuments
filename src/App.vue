<template>
    <div id="app">
      <img src="@/assets/media/bahad13icon.svg" alt="bahad13icon" class="bahad13-icon">
      <img src="@/assets/media/madorTil.svg" alt="madorTil" class="mador-til">
      <open-screen v-if="!isStart" class="open-screen"  @start="nextPage"></open-screen>
      <suspect-info v-if="isStart" class="suspect-info"></suspect-info>
    </div>

</template>

<script>
import OpenScreen from '@/components/OpenScreen.vue';
import SuspectInfo from '@/components/SuspectInfo.vue';


export default {
  name: "app",
  components: {
    OpenScreen,
    SuspectInfo
  },
  data() {
      return {
          isStart: false,
      };
  },
  methods: {
    nextPage() {
      this.isStart = true;
    }
  }
}
</script>

<style>
#app {
  background-size: 100vw 100vh;
  height: 100vh;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  direction: rtl;
  overflow: hidden;
    background-color: #0E2C8E;
}
/* .open-screen {
  height: 100vh;
  width: 100vw;
} */
.suspect-info
html {
  font-size: calc(10px + 0.5vw);
}
@font-face {
  font-family: "dana";
  src: url("@/assets/fonts/DanaYadAlefAlefAlef-Normal.otf");
}
@font-face {
  font-family: "rubik";
  src: url("@/assets/fonts/Rubik-Regular.ttf");
}
@font-face {
  font-family: "abraham";
  src: url("@/assets/fonts/Abraham-Regular.ttf");
}

.bahad13-icon {
    position: fixed;
    width: 5rem;
    top: 1rem;
    left: 1rem;
}
.mador-til {
    position: fixed;
    bottom: 1rem;
    right: 1%;
    width: 6rem;
}

</style>
