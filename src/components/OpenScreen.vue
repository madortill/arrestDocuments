<template>
  <div id="open-screen">
    <div class="container">
      <notebook @start="nextPage" class="notebook"></notebook>
    </div>
    <about></about>
  </div>
</template>

<script>
import Notebook from "@/components/Notebook.vue";
import About from "@/components/About.vue";
export default {
  name: "open-screen",
  components: {
    Notebook,
    About,
  },
  data() {
    return {
      showAbout: false,
      clickBtn: 0,
    };
  },
  methods: {
    nextPage() {
      this.$emit("start");
    },
    // openAbout() {
    //   if (this.clickBtn % 2 === 0) {
    //     this.showAbout = true;
    //   } else {
    //     this.showAbout = false;
    //   }
    //   this.clickBtn++;
    // },
  },
};
</script>

<style scoped>
#open-screen {
  background-image: url("@/assets/media/endScreen/end.png");
  background-size: 100vw 100vh;
  height: 100vh;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  overflow: hidden;
}
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.title {
  font-family: "abraham";
  font-size: 2rem;
  color: white;
}
.noteBookContainer {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.notebook {
  margin-top: 7rem;
  animation: upDown 1.7s infinite;
}
@keyframes upDown {
  0% {
    margin-top: 7rem;
  }
  50% {
    margin-top: 6rem;
  }
  100% {
    margin-top: 7rem;
  }
}
@media (max-width: 650px) {
  .notebook {
        width: 30rem;
        position: relative;
        top: -5rem;
    }
}
@media (max-width: 320px) {
    .notebook {
        width: 25rem;
    }
}
</style>
