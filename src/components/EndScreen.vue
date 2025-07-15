<template>
  <div id="end-screen">
    <div class="end-container">
      <p class="endText">סיימתם למלא את כל מסמכי המעצר!</p>
      <p class="endText">בזכותכם עצירת החשוד הושלמה!</p>
      <button class="againBtn" @click="startAgain">לתחילת הלומדה</button>
    </div>
    <div class="graphic">
      <div class="car-container">
        <img src="@/assets/media/endScreen/policeCar.png" class="policeCar" alt="road" />
      </div>
      <img src="@/assets/media/endScreen/road.png" class="road" alt="road" />
      <div class="grass"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "end-screen",
  methods: {
    startAgain() {
      this.$emit("start-over");
    },
  },
};
</script>

<style scoped>
#end-screen {
  background-image: url("@/assets/media/endScreen/end.png");
  background-size: cover;
  height: 100vh;
  background-position: center;
  background-repeat: no-repeat;
  overflow: hidden;
}
.graphic {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100vh;
  position: relative;
}

.car-container {
  position: absolute;
  top: 3rem; /* שימי לב למיקום מעל הכביש */
  left: 100%; /* מתחילה מחוץ למסך מימין */
  width: 35rem;
  animation: drive 10s linear forwards; /* האנימציה */
  z-index: 3;
}

@keyframes drive {
  0% {
    left: 100%;
  }
  100% {
    left: -40rem; /* יוצאת שמאלה מחוץ למסך */
  }
}

.policeCar {
  width: 100%;
}

.road {
  width: 100rem;
  height: 5rem;
  position: relative;
  z-index: 2;
  margin-top: 10rem;
}
.end-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 5rem;
  padding: 2rem;
}
.endText {
  font-family: "rubik";
  font-size: 2rem;
  margin: 0.3rem;
  color: white;
  font-family: "abraham";
  text-align: center;

}
.againBtn {
  font-family: "rubik";
  font-weight: bold;
  font-size: 1.5rem;
  background-color: #be0000;
  padding: 1rem 2rem;
  border-radius: 1rem;
  color: white;
  cursor: pointer;
  border: none;
  margin-top: 3rem;
}
.againBtn:hover {
  background-color: #940000;
}
.againBtn:active {
  background-color: #d40000;
}
</style>
