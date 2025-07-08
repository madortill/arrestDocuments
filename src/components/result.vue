<template>
  <div id="result">
    <div v-if="resultFrom === 'right'" class="container">
      <p class="text right">כל הכבוד ענית נכון על כל השאלות!</p>
    </div>
    <div v-if="resultFrom === 'wrong'" class="container">
      <p class="text">יש שאלות שצריך לתקן...</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "result",
  props: ["resultFrom"],
  components: {},
  data() {
    return {};
  },
  methods: {},
};
</script>

<style scoped>
#result {
  background-size: 100vw 100vh;
  overflow: hidden;
}
.container {
  width: 10rem;
  height: 10rem;
  background-color: #0e2c8e;
  overflow: hidden;
  text-align: center;
  padding: 1rem;
  border-radius: 2rem;
  position: relative; /* מספיק כדי שz-index פנימי יעבוד אם צריך */
}
.text {
  font-family: "rubik";
  color: white;
  direction: rtl;
  position: relative;
  top: 1rem;
  right: 1.6rem;
  width: 7rem;
  font-size: 1.5rem;
}
.right {
  position: relative;
  top: 1rem;
  right: 1.2rem;
  width: 8rem;
}

.result {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 8; /* שיהיה מעל הכול */
  pointer-events: none; /* רשות: אם אתה לא רוצה לחסום אינטראקציה */
}
#back {
  background-color: #00000080;
  z-index: 5; /* יותר גבוה מהמסמכים */
  width: 100vw;
  height: 100vh;
  position: relative;
}
</style>
