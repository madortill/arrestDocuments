<template>
    <div id="suspect-info">
        <div class="container">
            <div class="finale-exe type-writer">
      <p
        v-for="(text, index) in array1"
        :key="text"
        :style="{
          '--delay': `${index * 2.5}s`,
          '--width': `${text.length}ch`,
          'font-size':'1.6rem',
        }"
        class="text-writer"
      >
        {{ text }}

      </p>
    </div>
            <img src="@/assets/media/suspectInfo/computer.svg" alt="computer" class="computer">
            <img src="@/assets/media/suspectInfo/suspect.svg" alt="computer" class="suspect">

            <p v-if="showBtn" class="continue-btn" @click = "toInterrogation">הבא</p>

        </div>
        
        
    </div>

</template>

<script>
export default {
  name: "suspect-info",
  components: {
  },
  data() {
     return{
        array1: [
            "הנחקר רב”ט נועם רייס,","מספר אישי 8859963,","שעת עצירה 13:00","משרת כטבח בבסיס בח”א 21,",  "חשוד בהטרדה מינית ומעשה מגונה בכוח.", "לאחר מספר שעות של חקירה,"," החשוד הודה בחשדות המיוחסים לו", "והוחלט לעצור אותו."
        ],
        showBtn: true,
     };
  },
  mounted() {
    // זמן כולל = מספר שורות * זמן דיליי לכל שורה (3.2s) + זמן אנימציה אחרונה (2s)
    const delayPerLine = 2.5;
    const typingDuration = 2;
    const totalDelay = (this.array1.length - 1) * delayPerLine + typingDuration;

    setTimeout(() => {
      this.showBtn = true;
    }, totalDelay * 1000); // הופך לשניות
  },
  methods: {
    toInterrogation () {
        this.$emit("next");
    }
  }
}
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: -18rem;
}
.computer {
    width: 42rem;
    align-items: center;
    margin-top: 3rem;
    margin-left: 30rem;
}
.suspect {
    margin-top: -30rem;
    margin-right: 40rem;
    width: 12rem;
}
.continue-btn {
    font-family: "rubik";
    font-weight: bold;
    font-size: 1.5rem;
    background-color: #BE0000;
    padding: 1rem 2rem;
    border-radius: 1rem;
    margin-right: 70rem;
    cursor: pointer;
}
.continue-btn:hover {
    background-color: #d40000;
}
.finale-exe {
    position: relative;
  width: 10%;
  height: 70%;
    top: 27rem;
  left: 30rem;
  /* bottom: 20%; */
  /* background: #000000; */
  border-radius: 50px;
  box-shadow: 0 15px 20px -20px rgba(0, 0, 0, 0.4);
  text-align: center;
  align-items: center;
  padding: 0 1rem;
}
.type-writer > p {
  animation: typeWrite 2s var(--delay) steps(30) normal both,
    blink 400ms var(--delay) steps(45) 6;
}
@keyframes typeWrite {
  from {
    width: 0%;
  }

  to {
    width: var(--width);
  }
}
.finale-exe > p {
  display: block;
  width: fit-content;
  white-space: nowrap;
  text-align: right;
  overflow: hidden;
  border-left: solid 3px transparent;
  max-width: fit-content;
  margin: 4%;
  color: white;
  font-family: "alefBold";
  text-align: center;
}
@keyframes blink {
  to {
    border-left-color: rgb(255, 255, 255);
  }

  from {
    border-left-color: transparent;
  }
}
@media (max-width: 1444px) {
    .computer {
    width: 40rem;
    align-items: center;
    margin-left: 18rem;
}
.suspect {
    margin-right: 47rem;
    width: 10rem;
}
.continue-btn {
    margin-right: 50rem;
    margin-top: 5rem;
}
.finale-exe {
    top: 26rem;
    left: 23rem;
}
    

/* @media (max-width: 940px) {

} */
}

</style>
