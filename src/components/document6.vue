<template>
  <div id="document6" :class="{ background: propsResult }">
    <result class="result" :resultFrom="propsResult" />
    <div class="details1">
      <input
        v-for="(answer, i) in userAnswers"
        :key="i"
        :id="'input' + i"
        type="text"
        class="input1"
        :class="{ wrong: wrongUserAnswers[i] }"
        v-model="userAnswers[i]"
      />
    </div>
    <div class="details2">
      <input
        v-for="(answer, i) in userAnswers1"
        :key="i"
        :id="'input' + i"
        type="text"
        class="input1"
        :class="{
          wrong: wrongUserAnswers1[i],
          'last-input1': i === userAnswers1.length - 1,
        }"
        v-model="userAnswers1[i]"
      />
    </div>
    <div class="reason">
      <input
        type="text"
        class="input2"
        :class="{ wrong: wrongReason }"
        v-model="reasonAnswer"
      />
    </div>
    <div class="no-public">
      <input
        type="text"
        class="input3"
        :class="{ wrong: wrongNoPublic }"
        v-model="publicDetails"
      />
    </div>
    <img
      src="@/assets/media/part1documents/signature2.svg"
      alt="signature"
      class="signature"
      id="signature"
      @click="sign"
      :class="{
        chosen: signed,
      }"
    />
    <button
      @click="backToMap"
      class="back-btn"
      :class="{ 'disabled-btn': !debugMode && !areAllFieldsFilled() }"
      :disabled="!debugMode && !areAllFieldsFilled()"
    >
      בדיקה
    </button>
  </div>
</template>

<script>
import result from "./result.vue";
export default {
  name: "document6",
  components: {
    result,
  },
  data() {
    return {
      userAnswers: Array(4).fill(""),
      userAnswers1: Array(4).fill(""),
      reasonAnswer: "",
      publicDetails: "",
      signed: false,
      userInfo1: ["נועם", "רייס", "שמואל", "רינת"],
      userInfo2: ["8859963", "טבח", 'בא"ח 21', "שדרות הערבה 16, בת חן"],
      checked: "",
      checked1: "",
      wrongUserAnswers: [false, false, false, false],
      wrongUserAnswers1: [false, false, false, false],
      wrongReason: "",
      wrongNoPublic: "",
      reason: "הטרדה מינית ומעשה מגונה בכוח",
      noPublic: "כלל חומרי החקירה",
      debugMode: false,
      propsResult: "",
    };
  },
  methods: {
    sign() {
      this.signed = true;
    },
    areAllFieldsFilled() {
      return (
        this.userAnswers.every((val) => val.trim() !== "") && // פרטי עצור 1
        this.userAnswers1.every((val) => val.trim() !== "") && // פרטי עצור 2
        this.reasonAnswer.trim() !== "" && // סיבה
        this.publicDetails.trim() !== "" && // "לא לפרסם"
        this.signed // חתימה
      );
    },
    backToMap() {
      if (this.debugMode) {
        this.$emit("next-doc");
        return;
      }
      let rightAns = 0;
      // פרטי עצור 1
      this.checked = true;
      let allCorrect = true;
      this.userAnswers.forEach((ans, i) => {
        const isCorrect = ans.trim() === this.userInfo1[i];
        this.wrongUserAnswers[i] = !isCorrect;
        if (!isCorrect) {
          allCorrect = false;
        }
      });
      if (allCorrect) {
        rightAns++;
      }

      //   פרטי עצור 2
      this.checked1 = true;
      let allCorrect1 = true;
      this.userAnswers1.forEach((ans, i) => {
        const isCorrect1 = ans.trim() === this.userInfo2[i];
        this.wrongUserAnswers1[i] = !isCorrect1;
        if (!isCorrect1) {
          allCorrect1 = false;
        }
      });
      if (allCorrect) {
        rightAns++;
      }

      //   סיבה
      if (this.reasonAnswer.trim() === this.reason) {
        this.wrongReason = false;
        rightAns++;
      } else {
        this.wrongReason = true;
      }

      //   לא לפרסם
      if (this.publicDetails.trim() === this.noPublic) {
        this.wrongNoPublic = false;
        rightAns++;
      } else {
        this.wrongNoPublic = true;
      }

      //   תוצאה סופית
      if (rightAns === 4) {
        this.propsResult = "right";
        this.$emit("result", true);
        setTimeout(() => {
          this.$emit("result", false);
          alert("yayyy");
        }, 2200);
      } else {
        this.propsResult = "wrong";
        this.$emit("result", true);
        setTimeout(() => {
          this.propsResult = "";
          this.$emit("result", false);
        }, 2200);
      }
    },
    // check() {
    //     this.checked = true;
    //   let allCorrect = true;
    //   this.userAnswers.forEach((ans, i) => {
    //     const isCorrect = ans.trim() === this.userInfo1[i];
    //     this.wrongUserAnswers[i] = !isCorrect;
    //     if (!isCorrect) {
    //       allCorrect = false;
    //     }
    //   });
    //   if (allCorrect) {
    //     console.log("yayyy");
    //   }
    // },
    // check1() {
    //     this.checked1 = true;
    //   let allCorrect = true;
    //   this.userAnswers1.forEach((ans, i) => {
    //     const isCorrect = ans.trim() === this.userInfo2[i];
    //     this.wrongUserAnswers1[i] = !isCorrect;
    //     if (!isCorrect) {
    //       allCorrect = false;
    //     }
    //   });
    //   if (allCorrect) {
    //     console.log("yayyy");
    //   }
    // },
    // check2() {
    //     if (this.reasonAnswer.trim() === this.reason) {
    //     this.wrongReason = false;
    //     console.log("yayyy");
    //   } else {
    //     this.wrongReason = true;
    //   }
    // },
    // check3() {
    //     if (this.publicDetails.trim() === this.noPublic) {
    //     this.wrongNoPublic = false;
    //     console.log("yayyy");
    //   } else {
    //     this.wrongNoPublic = true;
    //   }
    // },
  },
};
</script>

<style scoped>
#document6 {
  width: 40rem;
  height: 45rem;
  background-image: url("@/assets/media/part3documents/publication.svg");
  background-size: 100% 100%;
  background-repeat: no-repeat;
}
.details1 {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 11.7rem;
  margin-right: 8rem;
  gap: 1.5rem;
}
.input1 {
  position: relative;
  width: 3rem;
  right: 1.5rem;
}
.last-input1 {
  width: 8rem;
}
.details2 {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 1.5rem;
  margin-right: 8rem;
  gap: 1.5rem;
}
.reason {
  display: flex;
  flex-direction: row;
  align-items: center;
}
.input2 {
  width: 15rem;
  position: relative;
  top: 3rem;
  right: 12rem;
}
.no-public {
  display: flex;
  flex-direction: row;
  align-items: center;
}
.input3 {
  width: 15rem;
  position: relative;
  top: 6.5rem;
  right: 10rem;
}
.signature {
  width: 4rem;
  position: relative;
  top: 18rem;
  right: 12.5rem;
  cursor: pointer;
  opacity: 0;
}
.chosen {
  opacity: 1;
}
.wrong {
  border: 2px solid red;
  background-color: #ffe5e5;
}
.back-btn {
  position: absolute;
  bottom: 3rem;
  left: -3rem;
  border: none;
  width: 5rem;
  text-align: center;
  color: white;
  font-size: 1rem;
  font-weight: bold;
  border-radius: 1rem;
  font-family: "rubik";
  padding: 1rem;
  background-color: #0e2c8e;
  cursor: pointer;
}
.back-btn:hover {
  background-color: #0e277a;
}
.back-btn:active {
  background-color: #123199;
}
.disabled-btn {
  opacity: 0.5;
  pointer-events: none;
  cursor: not-allowed;
}
.result {
  position: fixed; /* במקום absolute */
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 999; /* שיהיה מעל הכול */
  pointer-events: none; /* רשות: אם אתה לא רוצה לחסום אינטראקציה */
}

</style>
