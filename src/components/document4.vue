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
      <button class="back-btn" :disabled="!areAllFieldsFilled()" :class="{ 'disabled-btn': !areAllFieldsFilled()}" @click="backToMap">בדיקה</button>
</div>
</template>

<script>
export default {
  name: "document2",
  components: {},
  data() {
    return {
      userAnswers: Array(3).fill(""),
      userAnswers2: Array(2).fill(""),
      userAnswers3: Array(4).fill(""),
      signed1: '',
      signed2: '',
      selectedDate: ["25", "06", "05"],
      wrongInputs: [false, false, false],
      selectedTime: "",
      checked: false,
      isCorrect: false,
      userInfo: ["8859963", 'רב"ט', "נועם רייס", 'בא"ח 21'],
      wrongUserAnswers3: [false, false, false, false, false], // לשמירת סטטוס טעויות
      checked3: false,
      reason: "הטרדה מינית ומעשה מגונה בכוח.",
      reasonAnswer: "",
      wrongReason: false,
      testimony: '"אני צריך חולצות, תחתונים וכדורי האלרגיה שלי"',
      wrongTestimony: false,
      testimonyAnswer: "",
     
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
        this.testimonyAnswer.trim() !== "" && // עדות מולאה
        (this.signed1 && this.signed2) // חתימה קיימת
      );
    },
    backToMap() {
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
        alert("כל התשובות נכונות!");
        this.$emit("backToTable");
      } else {
        alert("צריך לתקן חלק מהתשובות");
      }
    },
  }
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
  margin-right: 2rem; /* או כל גודל שתרצי */
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
.back-btn {
  position: absolute;
  bottom: 3rem;
  left: 0rem;
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
</style>
