<template>
  <div id="document4">
    <div class="que1-date">
      <input
        v-for="(answer, i) in userAnswers"
        :key="i"
        :id="'input' + i"
        type="text"
        class="input1"
        :class="{ wrong: wrongInputs[i] }"
        v-model="userAnswers[i]"
      />
      <input
        type="text"
        v-model="selectedTime"
        class="input2"
        :class="{ wrong: checked && !isCorrect }"
      />
    </div>
    <div class="que1-details">
      <input
        v-for="(answer3, i) in userAnswers3"
        :key="i"
        :id="'input' + i"
        type="text"
        class="input3"
        :class="{
          wrong: checked3 && wrongUserAnswers3[i],
          'last-input3': i === userAnswers3.length - 1,
        }"
        v-model="userAnswers3[i]"
      />
    </div>
    <div class="que1-text">
      <input
        type="text"
        class="input4"
        :class="{ wrong: wrongReason }"
        v-model="reasonAnswer"
      />
    </div>
    <div class="que2-text">
      <input
        type="text"
        class="input5"
        :class="{ wrong: wrongTestimony }"
        v-model="testimonyAnswer"
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
    <div class="container-details">
      <p class="detailBtn" @click="isOpen = !isOpen">
        {{ isOpen ? "סגירה" : "פרטים" }}
      </p>
      <details-box v-show="isOpen" :note="4" class="details"></details-box>
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
    <information class="information" :docNum="doc"></information>
    <img
      src="@/assets/media/part3documents/talk.png"
      class="conversion-btn"
      @click="backToDetails"
      alt="talk"
    />
    <p class="nextToBtn">*שימו לב יש בשיחה פרטים רלוונטים למילוי המסמך</p>
    <!-- <p class="conversion-btn" @click="backToDetails">חזרה לשיחה</p> -->
  </div>
</template>

<script>
import Information from "./Information.vue";
import DetailsBox from "./DetailsBox.vue";
export default {
  name: "document2",
  components: {
    Information,
    DetailsBox,
  },
  data() {
    return {
      userAnswers: Array(3).fill(""),
      userAnswers2: Array(2).fill(""),
      userAnswers3: Array(4).fill(""),
      signed1: "",
      signed2: "",
      selectedDate: ["25", "06", "05"],
      wrongInputs: [false, false, false],
      selectedTime: "",
      checked: false,
      isCorrect: false,
      userInfo: ["8859963", 'רב"ט', "נועם רייס", 'בא"ח 21'],
      wrongUserAnswers3: [false, false, false, false, false], // לשמירת סטטוס טעויות
      checked3: false,
      reason: "הטרדה מינית ומעשה מגונה בכוח",
      reasonAnswer: "",
      wrongReason: false,
      testimony: '"אני צריך חולצות, תחתונים ואת כדורי האלרגיה שלי"',
      wrongTestimony: false,
      testimonyAnswer: "",
      debugMode: false,
      doc: 0,
      DOC_NUM: 1,
      isOpen: false,
      isInfoOpen: false,
      showRed: false,
    };
  },
  methods: {
    sign(event) {
      if (event.target.id === "signature1") {
        this.signed1 = true;
      } else {
        this.signed2 = true;
      }
    },
    validateAllFields() {
      return (
        this.userAnswers.every((val) => val.trim() !== "") && // תאריך מולא
        this.selectedTime.trim() !== "" && // שעה נבחרה
        this.userAnswers3.every((val) => val.trim() !== "") && // פרטי העצור מולאו
        this.reasonAnswer.trim() !== "" && // סיבה מולאה
        this.testimonyAnswer.trim() !== "" && // עדות מולאה
        this.signed1 &&
        this.signed2 // חתימה קיימת
      );
    },
    nextDoc() {
      if (this.debugMode) {
        this.$emit("next-doc");
        return;
      }
      let rightAns = 0;

      // בדיקת תאריך
      if (
        this.userAnswers.every((val, index) => val === this.selectedDate[index])
      ) {
        rightAns++;
      }
      this.wrongInputs = this.userAnswers.map(
        (val, index) => val !== this.selectedDate[index]
      );

      // בדיקת שעה
      this.checked = true;
      this.isCorrect = this.selectedTime === "13:20";
      if (this.isCorrect) {
        rightAns++;
      }

      // בדיקת פרטי העצור
      this.checked3 = true;
      let allCorrect = true;
      this.userAnswers3.forEach((ans, i) => {
        const isCorrect = ans.trim() === this.userInfo[i];
        this.wrongUserAnswers3[i] = !isCorrect;
        if (!isCorrect) {
          allCorrect = false;
        }
      });
      if (allCorrect) {
        rightAns++;
      }

      // בדיקת סיבה
      if (this.reasonAnswer.trim() === this.reason) {
        this.wrongReason = false;
        rightAns++;
      } else {
        this.wrongReason = true;
      }

      // בדיקת עדות
      if (this.testimonyAnswer.trim() === this.testimony) {
        this.wrongTestimony = false;
        rightAns++;
      } else {
        this.wrongTestimony = true;
      }

      // בדיקת חתימה
      if (!this.signed1 && !this.signed2) {
        alert("וודאו שהקפתם את אפשרות הנכונה וחתמתם");
      } else {
        rightAns++;
      }

      // סיכום התוצאה
      if (rightAns === 6) {
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
        this.doc = 4;
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
#document4 {
  width: 40rem;
  height: 45rem;
  background-image: url("@/assets/media/part3documents/arrestHearing.svg");
  background-size: 100% 100%;
  background-repeat: no-repeat;
}
.que1-date {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 8.1rem;
  margin-right: 11.7rem;
  gap: 0.3rem;
}
.input1 {
  width: 0.8rem;
}
.input2 {
  position: relative;
  width: 2.5rem;
  right: 1.5rem;
}
.que1-details {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 7rem;
  gap: 0.9rem;
}
.input3 {
  width: 3.5rem;
  position: relative;
  top: -6.8rem;
  right: 8.8rem;
}
.last-input3 {
  margin-right: 2rem;
}
.input4 {
  width: 15rem;
  position: relative;
  top: -4.8rem;
  right: 11rem;
}
.input5 {
  width: 15rem;
  position: relative;
  right: 11rem;
  top: 0.5rem;
}
.signature1 {
  width: 4rem;
  position: relative;
  top: 15.8rem;
  right: 25.5rem;
  cursor: pointer;
  opacity: 0;
}
.signature2 {
  width: 4rem;
  position: relative;
  top: 15.5rem;
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
  left: 6rem;
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
  top: 3rem;
  left: -6.5rem;
  cursor: pointer;
}
.nextToBtn {
  width: 10rem;
  text-align: center;
  position: relative;
  top: -3rem;
  left: -10rem;
  font-size: 0.8rem;
  font-family: "rubik";
}
.show {
  opacity: 1;
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
@media (max-width: 1350px) {
  .que1-date {
    margin-top: 7.8rem;
    margin-right: 11.5rem;
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
  .que1-date {
    margin-right: 11.3rem;
  }
  .input1 {
    height: 0.8rem;
  }
  .input2 {
    height: 0.8rem;
  }
}
@media (max-width: 870px) {
  .information {
    right: 13rem;
  }
  .details {
    right: 25rem;
  }
}
@media (max-width: 610px) {
  .information {
    right: 15.5rem;
  }
  .details {
    right: 21.3rem;
  }
  .detailBtn {
    right: 22rem;
  }
  .infoBtn {
    left: 20rem;
  }
  .input3 {
    height: 0.8rem;
    position: relative;
  }
  .signature1 {
    top: 15rem;
  }
  .signature2 {
    top: 14.8rem;
  }
}
@supports (-webkit-touch-callout: none) {
  @media (max-width: 610px) {
    .que1-date {
      margin-top: 7.6rem;
      gap: 0.2rem;
    }
    .input1 {
      width: 0.6rem;
    }
    .input2 {
      position: relative;
      width: 2.3rem;
      right: 0.8rem;
    }
  }
}
</style>
