<template>
  <div id="document2">
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
      <div class="que1-text">
        <input
          type="text"
          class="input4"
          v-model="reasonAnswer"
          :class="{ wrong: wrongReason }"
        />
      </div>
      <div class="que1-hours">
        <input
          type="text"
          class="input5"
          v-model="hourAnswer"
          :class="{ wrong: wrongHours }"
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
    </div>
    <div class="contaner-details">
      <p class="detailBtn" @click="isOpen = !isOpen">פרטים</p>
      <details-box v-show="isOpen" :note="2" class="details"></details-box>
    </div>
    <button
      class="back-btn"
      :disabled="!debugMode && !areAllFieldsFilled()"
      :class="{ 'disabled-btn': !debugMode && !areAllFieldsFilled() }"
      @click="backToMap"
    >
      לחדר החקירה
    </button>
    <!-- <div class="info-container">
      <p class="time-info">הודיעו לי על זכויותיי בשעה 13:04</p>
    </div>
    <img
      src="@/assets/media/suspectInfo/suspect.svg"
      alt="computer"
      class="suspect"
    /> -->
    <button class="infoBtn" @click="openInfo">דגשים למילוי המסמך</button>
    <information class="information" :docNum="doc"></information>
  </div>
</template>

<script>
import Information from './Information.vue';
import DetailsBox from "./DetailsBox.vue";
export default {
  name: "document2",
  components: {
    Information,
    DetailsBox
  },
  data() {
    return {
      userAnswers: Array(3).fill(""),
      userAnswers2: Array(2).fill(""),
      userAnswers3: Array(5).fill(""),
      selectedTime: "",
      checked: false,
      isCorrect: false,
      selectedDate: ["25", "06", "05"],
      wrongInputs: [false, false, false], // חדש
      userInfo: ["8859963", 'רב"ט', "נועם רייס", "טבח", 'בא"ח 21'],
      wrongUserAnswers3: [false, false, false, false, false], // לשמירת סטטוס טעויות
      checked3: false,
      reason: "הטרדה מינית ומעשה מגונה בכוח",
      reasonAnswer: "",
      wrongReason: false,
      hours: "18",
      wrongHours: false,
      hourAnswer: "",
      signed1: false,
      signed2: false,
      debugMode: true,
      doc: 0,
      isOpen: false,
    };
  },

  methods: {
    sign(event) {
      if (event.target.id === "signature1") {
        this.signed1 = true;
        console.log(this.signed1);
      } else {
        this.signed2 = true;
        console.log(this.signed2);
      }
    },
    areAllFieldsFilled() {
      return (
        this.userAnswers.every((val) => val.trim() !== "") && // תאריך מולא
        this.selectedTime.trim() !== "" && // שעה נבחרה
        this.userAnswers3.every((val) => val.trim() !== "") && // פרטי העצור מולאו
        this.reasonAnswer.trim() !== "" && // סיבה מולאה
        this.hourAnswer.trim() !== "" && // שעות מולאו
        this.signed1 &&
        this.signed2 // חתימה קיימת
      );
    },
    normalizeText(text) {
      return text
        .replace(/[\u2018\u2019\u0060\u00B4\u02BC]/g, "'") // אפוסטורופים
        .replace(/[\u201C\u201D]/g, '"') // גרשיים חכמים
        .replace(/[\u05F4]/g, '"') // גרשיים בעברית (״)
        .replace(/["']/g, "'") // המרה אחידה לגרש בודד
        .trim();
    },

    backToMap() {
      if (this.debugMode) {
        this.$emit("backToTable");
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
      this.isCorrect = this.selectedTime === "13:04";
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

      // בדיקת שעות
      if (this.hourAnswer.trim() === this.hours) {
        this.wrongHours = false;
        rightAns++;
      } else {
        this.wrongHours = true;
      }

      // בדיקת חתימה
      if (!this.signed1 && !this.signed2) {
        alert("וודאו שהקפתם את אפשרות הנכונה וחתמתם");
      } else {
        rightAns++;
      }

      // סיכום התוצאה
      if (rightAns === 6) {
        alert("כל התשובות נכונות!");
        this.$emit("backToTable");
      } else {
        alert("צריך לתקן חלק מהתשובות");
      }
    },
    openInfo() {
      if(this.doc === 0) {
        this.doc = 2;
      } else {
        this.doc = 0;
      }
    },
  },
};
</script>

<style scoped>
#document2 {
  width: 40rem;
  height: 43rem;
  background-image: url("@/assets/media/part1documents/explainRights.svg");
  background-size: 100% 100%;
  background-repeat: no-repeat;
}
.info-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  margin-top: -13rem;
  margin-right: -15rem;
  width: 13rem;
  height: 13rem;
  background-image: url("@/assets/media/part1documents/talkBubble.svg");
  background-size: 100% 100%;
  background-repeat: no-repeat;
}
.time-info {
  width: 8rem;
  position: relative;
  top: 3rem;
  right: 1rem;
  font-family: "rubik";
}

.suspect {
  margin-top: -5rem;
  margin-right: -22rem;
  width: 12rem;
}
.que1-date {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 8rem;
  margin-right: 11.9rem;
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
  gap: 0.5rem;
}
.input3 {
  width: 3.5rem;
  position: relative;
  top: -7.9rem;
  right: 8.8rem;
}
.last-input3 {
  margin-right: 2rem; /* או כל גודל שתרצי */
}
.input4 {
  width: 15rem;
  position: relative;
  top: -5rem;
  left: 14rem;
}
.input5 {
  width: 2rem;
  position: relative;
  top: -3rem;
  left: 22.5rem;
}
.wrong {
  border: 2px solid red;
  background-color: #ffe5e5;
}
.signature1 {
  width: 4rem;
  position: relative;
  top: 17rem;
  left: 17rem;
  cursor: pointer;
  opacity: 0;
}
.signature2 {
  width: 4rem;
  position: relative;
  top: 17rem;
  left: 35.5rem;
  cursor: pointer;
  opacity: 0;
}
.chosen {
  opacity: 1;
}
.back-btn {
  position: absolute;
  bottom: 0.2rem;
  left: 5rem;
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
.infoBtn {
  position: absolute;
  bottom: 39rem;
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
@media (max-width: 1455px) {
  .input3 {
  position: relative;
  top: -8rem;
}
.last-input3 {
  margin-right: 2rem; /* או כל גודל שתרצי */
}
}
@media (max-width: 930px) {
  .detailBtn {
    top: -4.5rem;
    right: 28rem;
  }
  .details {
    top: -0.5rem;
    right: 30rem;
  }
  .infoBtn {
    bottom: 44rem;
    left: 23rem;
  }
  .information {
    position: absolute;
    top: -7rem;
    right: 8rem;
  }
}
@media (max-width: 870px) {
  .information {
    right: 10rem;
  }
  .details {
    right: 25rem;
  }
}
@media (max-width: 610px) {
  .information {
    right: 16rem;
  }
  .details {
    right: 21rem;
  }
  
}

</style>
