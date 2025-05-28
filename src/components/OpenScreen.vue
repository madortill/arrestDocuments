<template>
  <div id="open-screen">
    <div class="container">
      <notebook @start="nextPage" class="notebook"></notebook>
      <!-- <div class="noteBookContainer">
                <img src="@/assets/media/openingPage/noteBook.svg" alt="">
            </div> -->
      <!-- <p class="startBtn">לחצו כדי להתחיל לחקור!</p> -->
    </div>
    <button class="aboutBtn" @click="openAbout">i</button>
    <Transition  name="fade"> 
      <div v-show="showAbout" class="div-about">
        <h3 class="list-text-about">מפתחת ראשית:</h3>
        <p class="list-text-about">טור' מאיה מרום</p>
        <h3 class="list-text-about">גרפיקה:</h3>
        <p class="list-text-about">סמל קריסטינה ברחטוב</p>
        <h3 class="list-text-about">מומחת תוכן:</h3>
        <p class="list-text-about">רעות</p>
        <h3 class="list-text-about">רמ"ד טי"ל:</h3>
        <p class="list-text-about">רס"מ עדן בן חמו</p>
        <h3 class="list-text-about">גרסה:</h3>
        <p class="list-text-about">יוני 2025</p>
      </div>
    </Transition>
  </div>
</template>

<script>
import Notebook from "@/components/Notebook.vue";
export default {
  name: "open-screen",
  components: {
    Notebook,
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
    openAbout() {
      if (this.clickBtn % 2 === 0) {
        this.showAbout = true;
      } else {
        this.showAbout = false;
      }
      this.clickBtn++;
    },
  },
};
</script>

<style scoped>
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
.aboutBtn {
  position: absolute;
  border: none;
  color: white;
  font-size: 1.6rem;
  transition: background-color 0.3s ease;
  background-color: #e10202;
  border-radius: 150px;
  width: 2%;
  height: 4%;
  cursor: pointer;
  left: 2.9%;
  top: 19%;
}

.aboutBtn:hover {
  background-color: #b90303;
}
.div-about {
  position: absolute;
  width: 12%;
  height: 40%;
  left: 10%;
  top: 8%;
  font-family: "rubik";
  background: #fff;
  border-radius: 1rem;
  box-shadow: 0 15px 20px -20px rgba(0, 0, 0, 0.4);
  text-align: center;
}

.list-text-about {
  transition: background-color 0.5s ease;
  margin: 5%;
}
.list-text-about:hover {
  background-color: #dbdbdb;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
.fade-enter-to,
.fade-leave-from {
  opacity: 1;
}

/* @media (max-width: 1444px) {
    note {
        width: ;
    }
} */
/* @media (max-width: 940px) {
    .notebook {
        width: 30rem;
        margin-top: 5.5rem;
    }
}
@media (max-width: 540px) {
    .notebook {
        width: 25rem;
        margin-top: 5.5rem;
    }
}
@media (max-width: 400px) {
    .notebook {
        width: 20rem;
        margin-top: 1rem;
    }
} */
</style>
