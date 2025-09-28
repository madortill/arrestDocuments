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
          }"
          class="text-writer"
        >
          {{ text }}
        </p>
      </div>
      <img :src="compImg" alt="computer" class="computer" />
      <img
        src="@/assets/media/suspectInfo/suspect.svg"
        alt="suspect"
        class="suspect"
      />

      <button 
  class="continue-btn" 
  :class="{ unable: !showBtn }" 
  :disabled="!showBtn" 
  @click="toInterrogation"
>
  הבא
</button>
    </div>
  </div>
</template>

<script>
import compImg from "@/assets/media/suspectInfo/computer.png";
export default {
  name: "suspect-info",
  components: {},
  data() {
    return {
      compImg,
      array1: [
        "הנחקר רב”ט נועם רייס,",
        "מספר אישי 8859963,",
        "נעצר ב5.6.2025 בשעה 13:00",
        "משרת כטבח בבסיס בא”ח 21,",
        "חשוד בהטרדה מינית ומעשה מגונה בכוח.",
        "לאחר מספר שעות של חקירה,",
        " החשוד הודה בחשדות המיוחסים לו",
        "והוחלט לעצור אותו.",
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
    toInterrogation() {
      this.$emit("next");
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: -18rem;
}
.computer {
  width: 95rem;
  align-items: center;
  margin-top: -0.3rem;
  margin-left: 55rem;
}
.suspect {
  margin-top: -49rem;
  margin-right: 38rem;
  width: 21rem;
  height: 27rem;
  background-image: url("@/assets/media/suspectInfo/backSuspect.png");
  background-size: 100% 100%;
  background-repeat: no-repeat;
}

.suspect-bg {
  margin-top: -55rem;
  margin-right: 38rem;
  width: 21rem;
  z-index: 1; /* אחורי */
  pointer-events: none; /* לא יפריע ללחיצות */
}
.continue-btn {
  font-family: "rubik";
  font-weight: bold;
  font-size: 1.5rem;
  background-color: #be0000;
  padding: 1rem 2rem;
  border-radius: 1rem;
  margin-right: 68rem;
  color: white;
  cursor: pointer;
  border: none;
}
.continue-btn:hover {
  background-color: #d40000;
}
continue-btn:disabled,
.continue-btn.unable {
  opacity: 0.5;
  cursor: not-allowed;
}

.continue-btn:disabled:hover,
.continue-btn.unable:hover {
  background-color: #be0000; /* נשאר בצבע המקורי */
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
  font-size: 1.6rem;
}
@keyframes blink {
  to {
    border-left-color: rgb(255, 255, 255);
  }

  from {
    border-left-color: transparent;
  }
}
.unable {
  opacity: 0.5;
  cursor: auto;
}
@media (max-width: 1444px) {
  .computer {
    width: 93rem;
    align-items: center;
    margin-top: -0.5rem;
    margin-left: 41rem;
  }
  .suspect {
    margin-right: 41rem;
    margin-top: -48rem;
    width: 20rem;
    height: 26rem;
  }
  .continue-btn {
    margin-right: 50rem;
    margin-top: 4rem;
  }
  .finale-exe {
    top: 26rem;
    left: 23rem;
  }
}

@media (max-width: 940px) {
  .computer {
    width: 60rem;
    align-items: center;
    margin-left: 27rem;
    margin-top: 17.2rem;
  }
  .suspect {
    margin-top: -32rem;
    margin-right: 27rem;
    width: 14rem;
    height: 18rem;
  }
  .continue-btn {
    margin-right: 25rem;
    margin-top: 4rem;
  }
  .finale-exe > p {
    font-size: 1.1rem;
  }
  .finale-exe {
    top: 35rem;
    left: 14.5rem;
  }
}
@media (max-width: 500px) {
  #suspect-info {
    overflow-x: none;
  }
  .computer {
    width: 60rem;
    align-items: center;
    margin-left: 13rem;
    margin-top: 12rem;
  }
  .suspect {
    margin-top: -10rem;
    margin-right: -0.5rem;
    width: 13rem;
  }
  .continue-btn {
    margin-right: -1rem;
    margin-top: 2rem;
  }
  .finale-exe > p {
    font-size: 1.1rem;
  }
  .finale-exe {
    top: 29.5rem;
    left: 9.5rem;
  }
}
@supports (-webkit-touch-callout: none) { 
  @media (max-width: 500px) {
  #suspect-info {
    overflow-x: none;
  }
  .computer {
    width: 60rem;
    align-items: center;
    margin-left: 13rem;
    margin-top: 10rem;
  }
  .suspect {
    margin-top: -10.4rem;
    margin-right: -0.5rem;
    width: 13rem;
  }
  .continue-btn {
    margin-right: -1rem;
    margin-top: 2rem;
  }
  .finale-exe {
    top: 28rem;
  }
}
}
</style>
