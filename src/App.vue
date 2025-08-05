<template>
    <div id="app">
      <img src="@/assets/media/bahad13icon.svg" alt="bahad13icon" class="bahad13-icon">
      <img src="@/assets/media/madorTil.svg" alt="madorTil" class="mador-til">
      <open-screen v-if="page === 0" class="open-screen"  @start="nextPage"></open-screen>
      <suspect-info v-if="page === 1" class="suspect-info" @next="toInterrogation"></suspect-info>
      <interrogation-room v-if="page === 2" @end-practice="endInvestigation" @saveName="saveName"></interrogation-room>
      <end-screen v-if="page === 3" @start-over="startAgain" :userName="userName"></end-screen>
    </div>

</template>

<script>
import OpenScreen from '@/components/OpenScreen.vue';
import SuspectInfo from '@/components/SuspectInfo.vue';
import InterrogationRoom from '@/components/InterrogationRoom.vue';
import EndScreen from '@/components/EndScreen.vue';


export default {
  name: "app",
  components: {
    OpenScreen,
    SuspectInfo,
    InterrogationRoom,
    EndScreen,
  },
  data() {
      return {
          page: 0,
          userName: '',
      };
  },
  methods: {
    nextPage() {
      this.page = 1;
    },
    toInterrogation() {
      this.page = 2;
    },
    endInvestigation() {
      this.page = 3;
    },
    startAgain() {
      this.page = 0;
    },
    saveName(theName) {
      this.userName = theName;
    },
  }
}
</script>

<style>
#app {
  background-image: url("@/assets/media/Artboard.png");
  background-size: 100vw 100vh;
  height: 100vh;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  direction: rtl;
  overflow-x: hidden;
  overflow-y: hidden;

}
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
@font-face {
  font-family: "alefBold";
  src: url("@/assets/fonts/Alef-bold.ttf");
}

.bahad13-icon {
    position: fixed;
    width: 5rem;
    top: 1rem;
    left: 1rem;
    z-index: 15;
}
.mador-til {
    position: fixed;
    bottom: 1rem;
    right: 1%;
    width: 5rem;
    z-index: 15;
}
@media (max-width: 610px) {
 #app {
    max-height: 91vh;
  }
}


</style>
