<template>
  <div id="document5">
    <div class="que1-details">
      <input
        v-for="(answer, i) in userAnswers"
        :key="i"
        :id="'input' + i"
        type="text"
        class="input1"
        :class="{
          'last-input1': i === userAnswers.length - 1,
          wrong: checked && wrongUserAnswers[i],
        }"
        v-model="userAnswers[i]"
      />
    </div>
    <div class="que1-date">
      <input
        v-for="(answer, i) in userAnswers1"
        :key="i"
        :id="'input' + i"
        type="text"
        class="input2"
        :class="{ wrong: wrongUserAnswers1[i] }"
        v-model="userAnswers1[i]"
      />
    </div>
    <div class="check-boxes">
      <input
        v-for="(answer, i) in checkBoxes1"
        :key="i"
        type="checkbox"
        class="check-box1"
        :id="'check1' + i"
      />
      <input
        v-for="(answer, i) in checkBoxes2"
        :key="i"
        type="checkbox"
        class="check-box2"
        :id="'check2' + i"
        v-model="isChecked[i]"
        @change="showTextBox"
      />
    </div>
    <div class="checkBox1-text" :class="{ none: !showContent1 }">
      <input
        type="text"
        class="input3"
        :class="{ wrong: wrongReason }"
        v-model="reasonAnswer"
      />
    </div>
    <div class="checkBox2-texts" :class="{ none: !showContent2 }">
      <!-- time -->
      <input
        type="text"
        v-model="startTime"
        class="input4"
        :class="{ wrong: checked && !isCorrect }"
      />
      <!-- mark -->
      <div
        class="mark"
        @click="choose"
        :class="{
          chosen: chosen,
        }"
      ></div>
      <input
        type="text"
        v-model="nameLawyer"
        class="input5"
        :class="{ wrong: wrongUserAnswers2.name }"
      />
      <input
        type="text"
        v-model="phoneNum"
        class="input6"
        :class="{ wrong: wrongUserAnswers2.phone }"
      />
      <input
        type="text"
        v-model="endTime"
        class="input7"
        :class="{ wrong: wrongUserAnswers2.time }"
      />
    </div>
    <img
      src="@/assets/media/part1documents/signature1.svg"
      alt="signature"
      class="signature1"
      id="signature1"
      @click="sign"
      :class="{
        chosen: signed1,
      }"
    />
    <img
      src="@/assets/media/part1documents/signature2.svg"
      alt="signature"
      class="signature2"
      id="signature2"
      @click="sign"
      :class="{
        chosen: signed2,
      }"
    />
    <div class="contaner-details">
      <p class="detailBtn" @click="isOpen = !isOpen">
        {{ isOpen ? "סגירה" : "פרטים" }}
      </p>
      <details-box v-show="isOpen" :note="5" class="details"></details-box>
    </div>
    <img
      src="@/assets/media/part1documents/nextBtn.png"
      @click="nextDoc"
      class="button-next"
      :disabled="!debugMode && !validateAllFields()"
      :class="{ 'disabled-btn': !debugMode && !validateAllFields() }"
      alt="btn"
    />
    <button class="infoBtn" @click="openInfo">
      {{ isInfoOpen ? "סגירה" : "דגשים למילוי" }}
    </button>
    <information :docNum="doc" class="information"></information>
    <img
      src="@/assets/media/part3documents/talk.png"
      class="conversion-btn"
      @click="backToDetails"
      alt="talk"
    />
  </div>
</template>

<script>
import Information from "./Information.vue";
import DetailsBox from "./DetailsBox.vue";
export default {
  name: "document5",
  components: {
    Information,
    DetailsBox,
  },
  data() {
    return {
      userAnswers: Array(4).fill(""),
      userAnswers1: Array(3).fill(""),
      checkBoxes1: Array(2).fill(""),
      checkBoxes2: Array(3).fill(""),
      isChecked: [],
      showContent1: false,
      showContent2: false,
      reasonAnswer: "",
      startTime: "",
      chosen: false,
      nameLawyer: "",
      phoneNum: "",
      endTime: "",
      signed1: false,
      signed2: false,
      userInfo: ["8859963", 'רב"ט', "נועם רייס", 'בא"ח 21'],
      checked: "",
      wrongUserAnswers: [false, false, false, false, false],
      selectedDate: ["25", "06", "05"],
      wrongUserAnswers1: [false, false, false],
      reason: "אני מתבייש",
      wrongReason: false,
      checked1: false,
      isCorrect: false,
      userInfo1: ["גלעד כהן", "0526648512", "13:19"],
      wrongUserAnswers2: [false, false, false],
      debugMode: true,
      doc: 0,
      DOC_NUM: 2,
      isOpen: false,
      isInfoOpen: false,
    };
  },
  methods: {
    showTextBox(event) {
      if (event.target.id === "check20") {
        this.showContent1 = !this.showContent1;
      } else if (event.target.id === "check21") {
        this.showContent2 = !this.showContent2;
      }
    },
    choose() {
      this.chosen = true;
    },
    sign(event) {
      if (event.target.id === "signature1") {
        this.signed1 = true;
      } else {
        this.signed2 = true;
      }
    },
    areAllFieldsFilled() {
      return (
        this.userAnswers.every((val) => val.trim() !== "") && // תשובות כלשהן
        this.userAnswers1.every((val) => val.trim() !== "") && // תאריך
        this.reasonAnswer.trim() !== "" && // סיבה
        this.startTime.trim() !== "" && // שעה
        this.nameLawyer.trim() !== "" && // שם עו"ד
        this.phoneNum.trim() !== "" && // טלפון
        this.endTime.trim() !== "" && // זמן סיום
        this.chosen && // בחירה קיימת
        this.signed1 && // חתימה 1
        this.signed2 // חתימה 2
      );
    },
    nextDoc() {
      if (this.debugMode) {
        this.$emit("next-doc");
        return;
      }

      let rightAns = 0;

      // בדיקת פרטי העצור
      this.checked = true;
      let allCorrect = true;
      this.userAnswers.forEach((ans, i) => {
        const isCorrect = ans.trim() === this.userInfo[i];
        this.wrongUserAnswers[i] = !isCorrect;
        if (!isCorrect) {
          allCorrect = false;
        }
      });
      if (allCorrect) {
        rightAns++;
      }

      // בדיקת תאריך
      if (
        this.userAnswers1.every(
          (val, index) => val === this.selectedDate[index]
        )
      ) {
        rightAns++;
      }
      this.wrongUserAnswers1 = this.userAnswers1.map(
        (val, index) => val !== this.selectedDate[index]
      );

      // סיבה
      if (this.reasonAnswer.trim() === this.reason) {
        this.wrongReason = false;
        rightAns++;
      } else {
        this.wrongReason = true;
      }

      //בודקת שעת התחלה
      this.checked = true;
      this.isCorrect = this.startTime === "13:11";
      if (this.isCorrect) {
        rightAns++;
      }

      this.wrongUserAnswers2.name =
        this.nameLawyer.trim() !== this.userInfo1[0];
      this.wrongUserAnswers2.phone = this.phoneNum.trim() !== this.userInfo1[1];
      this.wrongUserAnswers2.time = this.endTime.trim() !== this.userInfo1[2];

      const allCorrect1 =
        !this.wrongUserAnswers2.name &&
        !this.wrongUserAnswers2.phone &&
        !this.wrongUserAnswers2.time;

      if (allCorrect1) {
        rightAns++;
      }

      //   סיכום תוצאה ובדיקה סופית
      // if (rightAns === 5) {
      //   alert("כל התשובות נכונות!");
      //   this.$emit("next-doc");
      // } else {
      //   alert("צריך לתקן חלק מהתשובות");
      // }
      if (rightAns === 5) {
        this.$emit("result", "right");
        setTimeout(() => {
          this.$emit("result", "");
          this.$emit("next-doc");
        }, 2200);
      } else {
        this.$emit("result", "wrong");
        setTimeout(() => {
          this.$emit("result", "");
        }, 2200);
      }
    },
    openInfo() {
      if (this.doc === 0) {
        this.doc = 5;
      } else {
        this.doc = 0;
      }
      this.isInfoOpen = !this.isInfoOpen;
    },
    backToDetails() {
      this.$emit("to-details", this.DOC_NUM);
    },
  },
};
</script>

<style scoped>
#document5 {
  width: 40rem;
  height: 45rem;
  background-image: url("@/assets/media/part3documents/rights.svg");
  background-size: 100% 100%;
  background-repeat: no-repeat;
}
.que1-details {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 6.5rem;
  margin-right: 11.7rem;
  gap: 0.5rem;
}
.input1 {
  position: relative;
  width: 3rem;
  right: 1.5rem;
}
.last-input1 {
  margin-right: 2rem;
}
.que1-date {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 0.9rem;
  margin-right: 16rem;
  gap: 0.6rem;
}
.input2 {
  width: 0.8rem;
  height: 0.5rem;
  font-size: 0.7rem;
}
.check-boxes {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.6rem;
  width: 100%;
}
.check-box1 {
  accent-color: #474747;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 1.1rem;
  margin-left: 20rem;
  gap: 0.6rem;
}
.check-box2 {
  accent-color: #474747;
  align-items: center;
  margin-top: 1rem;
  position: relative;
  top: 2.5rem;
  margin-left: 20rem;
  gap: 1rem;
}
#check10 {
  accent-color: #ff0000;
}
#check11 {
  accent-color: #ff0000;
}
#check22 {
  accent-color: #ff0000;
}
.input3 {
  width: 6rem;
  position: relative;
  top: -4rem;
  right: 24rem;
}
.checkBox2-texts {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: -0.3rem;
}
.input4 {
  width: 2.5rem;
  margin-top: -4rem;
  margin-right: 14.5rem;
}
.none {
  visibility: hidden;
}
.mark {
  width: 2.3rem;
  height: 0.6rem;
  margin-top: -3.5rem;
  margin-left: 2.2rem;
  border: solid 2px #474747;
  border-radius: 20rem;
  cursor: pointer;
  opacity: 0;
}
.input5 {
  width: 4rem;
  height: 0.5rem;
  margin-top: -1.7rem;
  margin-right: -11.5rem;
  font-size: 0.7rem;
}
.input6 {
  width: 4rem;
  height: 0.5rem;
  margin-top: -1.7rem;
  margin-right: 2.3rem;
  font-size: 0.67rem;
}
.input7 {
  width: 1.7rem;
  height: 0.4rem;
  margin-right: -7.1rem;
  font-size: 0.67rem;
}
.signature1 {
  width: 4rem;
  position: relative;
  top: 12.5rem;
  right: 25.5rem;
  cursor: pointer;
  opacity: 0;
}
.signature2 {
  width: 4rem;
  position: relative;
  top: 12.5rem;
  right: 8rem;
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
.button-next {
  position: absolute;
  bottom: 2rem;
  left: 6.5rem;
  width: 2.2rem;
  cursor: pointer;
}
.disabled-btn {
  opacity: 0.5;
  pointer-events: none;
  cursor: not-allowed;
}
.infoBtn {
  position: absolute;
  bottom: 41rem;
  left: 36.5rem;
  border: none;
  width: 10rem;
  text-align: center;
  color: white;
  font-size: 1rem;
  font-weight: bold;
  border-radius: 1rem;
  font-family: "rubik";
  padding: 0.5rem;
  background-color: #0e2c8e;
  filter: drop-shadow(0 0 10px #0051ff);
  cursor: pointer;
}

.infoBtn:hover {
  background-color: #0e277a;
}
.infoBtn:active {
  background-color: #123199;
}
.conversion-btn {
  width: 5rem;
  text-align: center;
  position: relative;
  top: 4.5rem;
  left: -6.5rem;
  cursor: pointer;
}
.container-details {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.details {
  width: 10rem;
  position: absolute;
  top: 5rem;
  right: 36rem;
}

.detailBtn {
  position: absolute;
  height: 1rem;
  right: 36.5rem;
  top: 1rem;
  width: 5rem;
  z-index: 3;
  padding: 12px 0px;
  background-color: white;
  border-radius: 30%;
  text-align: center;
  color: white;
  font-size: 1rem;
  font-weight: bold;
  border-radius: 1rem;
  font-family: "rubik";
  background-color: #0e2c8e;
  filter: drop-shadow(0 0 10px #0051ff);
  cursor: pointer;
}
.detailBtn:hover {
  background-color: #0e277a;
}
.detailBtn:active {
  background-color: #123199;
}
@media (max-width: 1800px) {
  .checkBox2-texts {
    margin-top: -0.7rem;
  }
  .mark {
    margin-top: -3.3rem;
  }
}
@media (max-width: 1660px) {
  .checkBox2-texts {
    margin-top: -0.7rem;
  }
  .check-box1 {
    margin-top: 1rem;
  }
}
@media (max-width: 1550px) {
  .checkBox2-texts {
    margin-top: -0.9rem;
    margin-right: -0.2rem;
  }
  .check-box2 {
    position: relative;
    top: 2rem;
  }
  .mark {
    position: relative;
    right: 0.1rem;
  }
}
@media (max-width: 1430px) {
  .check-box1 {
    margin-top: 0.9rem;
  }
}
@media (max-width: 1340px) {
  .checkBox2-texts {
    margin-top: -1.1rem;
    margin-right: -0.2rem;
  }
}
@media (max-width: 1270px) {
  .que1-date {
    margin-top: 0.7rem;
  }
  .check-box2 {
    position: relative;
    top: 2.3rem;
  }
}
@media (max-width: 1170px) {
  .checkBox2-texts {
    margin-top: -1.35rem;
    /* margin-right: -0.2rem; */
  }
  /* .check-box2 {
  position: relative;
  top: 2rem;
} */
  /* .mark {
  position: relative;
  top: 0.2rem;
} */
}
@media (max-width: 1080px) {
  .check-box1 {
    margin-top: 0.78rem;
  }
  .que1-details {
    display: flex;
    flex-direction: row;
    align-items: center;
    margin-top: 6.5rem;
    margin-right: 11.7rem;
    gap: 0.5rem;
  }
}
@media (max-width: 1000px) {
  .que1-details {
    margin-top: 6.3rem;
  }
}
@media (max-width: 930px) {
  .detailBtn {
    top: -4.5rem;
    right: 30rem;
  }
  .details {
    top: -0.5rem;
    right: 27rem;
  }
  .infoBtn {
    bottom: 46rem;
    left: 25rem;
  }
  .information {
    position: absolute;
    top: -7rem;
    right: 8rem;
  }
  .checkBox2-texts {
    margin-top: -1.5rem;
    margin-right: -0.3rem;
  }
  .input4 {
    height: 0.5rem;
  }
}
@media (max-width: 870px) {
  .information {
    right: 13rem;
  }
  .details {
    right: 25rem;
  }
  .checkBox1-text {
    margin-top: -1rem;
    margin-right: -0.3rem;
  }
  .checkBox2-texts {
    margin-top: -0.9rem;
    margin-right: -0.4rem;
  }
}
@media (max-width: 785px) {
  #document5 {
    /* width: 42rem; */
    height: 49rem;
  }
  .checkBox2-texts {
    margin-top: -1rem;
    margin-right: -0.3rem;
  }
  .check-box2 {
    position: relative;
    top: 2rem;
  }
  .que1-details {
    margin-top: 7rem;
    margin-right: 11rem;
    gap: 1rem;
  }
  .que1-date {
    margin-top: 1rem;
    margin-right: 15.5rem;
    /* gap: 1rem; */
  }
  .checkBox2-texts {
    margin-top: -0.2rem;
    margin-right: -0.4rem;
  }
  .input1 {
    width: 2.8rem;
    height: 0.8rem;
  }
  .input3 {
    /* width: 2.8rem; */
    height: 0.8rem;
  }
  .input4 {
    width: 2rem;
    position: relative;
    right: 0.1rem;
    top: 0.3rem;
  }
  .input5 {
    width: 3rem;
    position: relative;
    right: -0.2rem;
    top: 0.3rem;
  }
  .input6 {
    width: 3.35rem;
    position: relative;
    right: 1.3rem;
    top: 0.2rem;
    font-size: 0.62rem;
  }
  .input7 {
    width: 1.5rem;
    position: relative;
    right: 1.5rem;
    top: 0.2rem;
    font-size: 0.62rem;
  }
  .mark {
    position: relative;
    top: 0.15rem;
    right: 0.5rem;
    width: 2.5rem;
  }
  .check-box1 {
    margin-top: 0.9rem;
    margin-right: -2rem;
  }
  .check-box2 {
    position: relative;
    top: 2.6rem;
    right: -1rem;
  }
  .conversion-btn {
    top: 6rem;
  }
  .signature1 {
    top: 14rem;
  }
  .signature2 {
    top: 14rem;
  }
  .infoBtn {
    bottom: 49.8rem;
  }
}
@media (max-width: 660px) {
  .mark {
    position: relative;
    top: -0.08rem;
  }
}
@media (max-width: 610px) {
  .information {
    right: 15.8rem;
  }
  .details {
    right: 21rem;
  }
  .detailBtn {
    right: 22rem;
  }
  .infoBtn {
    left: 20rem;
  }
  .checkBox2-texts {
    margin-top: -0.4rem;
    margin-right: -0.4rem;
  }
}
@media (max-width: 520px) {
  .checkBox2-texts {
    margin-top: -0.7rem;
    margin-right: -0.4rem;
  }
  .check-box2 {
    top: 2.3rem;
  }
}
@media (max-width: 450px) {
  .checkBox2-texts {
    margin-top: -0.9rem;
    margin-right: -0.4rem;
  }
  .input7 {
    right: 1rem;
  }
}
@media (max-width: 380px) {
  .checkBox2-texts {
    margin-top: -1.1rem;
    margin-right: -0.4rem;
  }
  .check-box2 {
    top: 2.1rem;
  }
}
@media (max-width: 320px) {
  .checkBox2-texts {
    margin-top: -1.2rem;
    margin-right: -0.5rem;
  }
}
@supports (-webkit-touch-callout: none) {
  @media (max-width: 450px) {
    .check-box2 {
      top: 1rem;
    }
    .checkBox2-texts {
    margin-top: -1.3rem;
    margin-right: -0.8rem;
  }
  .checkBox1-text {
    margin-top: -3rem;
  }
  /* .check-box1 {
    margin-top: 0.9rem;
  } */
  }
}
</style>
