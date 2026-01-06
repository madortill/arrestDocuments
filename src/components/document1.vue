<template>
  <div id="part1-documents" :class="background">
    <div v-if="page === 1" class="document1">
      <div
        class="marking2"
        id="solider"
        @click="choose"
        :class="{
          chosen: chosen === 'solider',
        }"
      ></div>
      <div class="que1">
        <input
          type="text"
          ref="0"
          class="input"
          v-model="pNum"
          @input="updateWrongCount"
          :class="pNum === '' ? '' : { wrong: !checkInput(pNum) }"
        />
        <select
          id="rank1"
          ref="1"
          v-model="selectedRan1k"
          class="input"
          style="width: 2.9rem"
        >
          <option v-for="rank in ranks" :key="rank" :value="rank" class="input">
            {{ rank }}
          </option>
        </select>
        <input
          type="text"
          ref="3"
          class="input"
          v-model="lastName"
          :class="
            lastName === '' ? '' : { wrong: containsNumber(lastName) }
          "
        />
        <input
          type="text"
          ref="4"
          class="input"
          v-model="firstName"
          :class="
            firstName === '' ? '' : { wrong: containsNumber(firstName) }
          "
        />
        <select
          id="forse1"
          ref="5"
          v-model="selectedForse1"
          class="input"
          style="width: 3.3rem"
        >
          <option
            v-for="forse in forses"
            :key="forse"
            :value="forse"
            class="input bla"
          >
            {{ forse }}
          </option>
        </select>
        <input type="text" ref="6" class="input" />
        <input
          type="text"
          ref="7"
          v-model="role"
          class="input"
          :class="
            role === '' ? '' : { wrong: containsNumber(role) }
          "
        />
      </div>
      <div class="que2">
        <input
          v-for="(answer, i) in userAnswers"
          :key="i"
          :id="'input' + i"
          type="text"
          class="input"
          v-model="userAnswers[i]"
          :class="{ wrong: wrongUserAnswers[i] }"
        />
      </div>
      <div class="que3">
        <input
          type="text"
          class="input3"
          v-model="reasonAnswer"
          :class="{ wrong: wrongReason }"
        />
      </div>

      <div class="que4">
        <select
          v-model="answers.que4.time"
          class="input4"
          id="time4"
          :class="{ wrong: wrongTimes.que4 }"
        >
          <option v-for="time in timeOptions" :key="time" :value="time">
            {{ time }}
          </option>
        </select>
        <select
          v-model="answers.que4.year"
          class="input4"
          :class="{ wrong: wrongDates.que4 }"
        >
          <option v-for="year in yearsArr" :key="year" :value="year">
            {{ year }}
          </option>
        </select>
        <select
          v-model="answers.que4.month"
          class="input4"
          :class="{ wrong: wrongDates.que4 }"
        >
          <option v-for="month in monthArr" :key="month" :value="month">
            {{ month }}
          </option>
        </select>
        <select
          v-model="answers.que4.day"
          class="input4"
          :class="{ wrong: wrongDates.que4 }"
        >
          <option v-for="day in dayArr" :key="day" :value="day">
            {{ day }}
          </option>
        </select>
      </div>
      <div class="que4-text">
        <input
          type="text"
          class="input"
          id="text4"
          v-model="roomUser"
          :class="{ wrong: wrongRoom }"
        />
      </div>
      <div class="que5">
        <select
          v-model="answers.que5.year"
          class="input4 input5"
          :class="{ wrong: wrongDates.que5 }"
        >
          <option v-for="year in yearsArr" :key="year" :value="year">
            {{ year }}
          </option>
        </select>
        <select
          v-model="answers.que5.month"
          class="input4 input5"
          :class="{ wrong: wrongDates.que5 }"
        >
          <option v-for="month in monthArr" :key="month" :value="month">
            {{ month }}
          </option>
        </select>
        <select
          v-model="answers.que5.day"
          class="input4 input5"
          :class="{ wrong: wrongDates.que5 }"
        >
          <option v-for="day in dayArr" :key="day" :value="day">
            {{ day }}
          </option>
        </select>
        <select
          v-model="answers.que5.time"
          class="input4 input5"
          id="time5"
          :class="{ wrong: wrongTimes.que5 }"
        >
          <option v-for="time in timeOptions" :key="time" :value="time">
            {{ time }}
          </option>
        </select>
      </div>
      <div class="que6">
        <select
          v-model="answers.que6.year"
          class="input4 input6"
          :class="{ wrong: wrongDates.que6 }"
        >
          <option v-for="year in yearsArr" :key="year" :value="year">
            {{ year }}
          </option>
        </select>
        <select
          v-model="answers.que6.month"
          class="input4 input6"
          :class="{ wrong: wrongDates.que6 }"
        >
          <option v-for="month in monthArr" :key="month" :value="month">
            {{ month }}
          </option>
        </select>
        <select
          v-model="answers.que6.day"
          class="input4 input6"
          :class="{ wrong: wrongDates.que6 }"
        >
          <option v-for="day in dayArr" :key="day" :value="day">
            {{ day }}
          </option>
        </select>
        <select
          v-model="answers.que6.time"
          class="input4 input6"
          id="time6"
          :class="{ wrong: wrongTimes.que6 }"
        >
          <option v-for="time in timeOptions" :key="time" :value="time">
            {{ time }}
          </option>
        </select>
      </div>
      <img
        src="@/assets/media/part1documents/signature1.svg"
        alt="signature"
        class="signature"
        id="signature"
        @click="sign"
        :class="{
          chosen: signed,
        }"
      />
    </div>
    <div class="contaner-details">
      <p class="detailBtn" @click="isOpen = !isOpen">{{ isOpen ? 'סגירה' : 'פרטים' }}</p>
      <details-box v-show="isOpen" :note="1" class="details"></details-box>
    </div>
    <img src="@/assets/media/part1documents/nextBtn.png" @click="nextDoc"
      class="button-next"
      :disabled="!debugMode && !validateAllFields()"
      :class="{ 'disabled-btn': !debugMode && !validateAllFields() }" alt="btn">
    <!-- <button
      @click="nextDoc"
      class="button-next"
      :disabled="!debugMode && !validateAllFields()"
      :class="{ 'disabled-btn': !debugMode && !validateAllFields() }"
    >
      לעמוד הבא
    </button> -->
    <button class="infoBtn" @click="openInfo">{{ isInfoOpen ? 'סגירה' : 'דגשים למילוי' }}</button>
    <information class="information" :docNum="doc"></information>
  </div>
</template>

<script>
import Information from "./Information.vue";
import DetailsBox from "./DetailsBox.vue";
export default {
  components: {
    Information,
    DetailsBox,
  },
  data() {
    return {
      inputs: [],
      reasonAnswer: "",
      roomUser: "",
      userAnswers: Array(7).fill(""),
      userInfo: ["8859963", 'רב"ט', "רייס", "נועם", "האוויר", 'בא"ח 21', "טבח"],
      page: 1,
      ranks: ["טוראי", 'רב"ט', "סמל", 'סמ"ר'],
      forses: [
        "היבשה",
        "האוויר",
        "הההנדסה",
        "הגנת גבולות",
        "החינוך והנוער",
        "משאבי האנוש",
        "החימוש",
        "הים",
        "הלוגיסטיקה",
        "המשטרה הצבאית",
        "הקשר והתקשוב",
        "הרבנות הצבאית",
        "הרגלים",
        "הרפואה",
        "השריון",
        "התותחנים",
        "המודיעין",
        "הכללי",
      ],
      reason: "צרכי חקירה",
      roomText: "כלא 10",
      pNum: "",
      lastName: "",
      firstName: "",
      userInput21: "",
      userInput22: "",
      userInput23: "",
      role: "",
      classes: [],
      chosen: "",
      signed: false,
      selectedYear: "",
      selectedMonth: "",
      selectedDay: "",
      timeOptions: [],
      yearsArr: [],
      monthArr: [],
      dayArr: [],
      answers: {
        que4: {
          year: "",
          month: "",
          day: "",
          time: "",
        },
        que5: {
          year: "",
          month: "",
          day: "",
          time: "",
        },
        que6: {
          year: "",
          month: "",
          day: "",
          time: "",
        },
      },
      wrongDates: {
        que4: false,
        que5: false,
        que6: false,
      },
      wrongTimes: {
        que4: false,
        que5: false,
        que6: false,
      },
      wrongUserAnswers: [],
      wrongReason: false,
      wrongRoom: false,
      wrongChosen: false,
      debugMode: false,
      propsResult: "",
      doc: 0,
      isOpen: false,
      isInfoOpen: false, 
    };
  },
  created() {
    this.generateTimeOptions();
    this.years();
    this.months();
    this.days();
  },
  methods: {
    validateAllFields() {
      const isValidID = this.checkInput(this.pNum);
      const isValidName1 =
        !this.containsNumber(this.lastName) &&
        this.lastName.trim() !== "";
      const isValidName2 =
        !this.containsNumber(this.firstName) &&
        this.firstName.trim() !== "";
      const isValidRoom =
        !this.containsNumber(this.role) &&
        this.role.trim() !== "";
      const allAnswersFilled = this.userAnswers.every(
        (ans) => ans.trim() !== ""
      );
      const allDateFieldsFilled = [
        this.answers.que4,
        this.answers.que5,
        this.answers.que6,
      ].every((ans) => ans.year && ans.month && ans.day && ans.time);

      return (
        this.signed &&
        this.chosen &&
        isValidID &&
        isValidName1 &&
        isValidName2 &&
        isValidRoom &&
        this.selectedRan1k &&
        this.selectedForse1 &&
        this.reasonAnswer.trim() !== "" &&
        this.roomUser.trim() !== "" &&
        allAnswersFilled &&
        allDateFieldsFilled
      );
    },
    normalize(text) {
  if (!text) return "";
  return text
    .toString()
    .trim()
    .replace(/[\"'״”“]/g, "")
    .replace(/\s+/g, " ")
    .toLowerCase();
},

isWrong(user, correct) {
  return this.normalize(user) !== this.normalize(correct);
},

isRight(user, correct) {
  return this.normalize(user) === this.normalize(correct);
},
nextDoc() {
  if (this.debugMode) {
    this.$emit("next-doc");
    return;
  }

  let rightAns = 0;

  if (!this.signed && !this.chosen) {
    alert("וודאו שהקפתם את אפשרות הנכונה וחתמתם");
  } else {
    rightAns++;
  }

  const allCorrect = this.userAnswers.every(
    (ans, i) => this.isRight(ans, this.userInfo[i])
  );

  if (allCorrect) rightAns++;

  if (this.isRight(this.reasonAnswer, this.reason)) rightAns++;

  if (
    this.answers.que4.time === "13:00" &&
    this.answers.que5.time === "13:00"
  ) rightAns++;

  if (this.answers.que6.time === "07:00") rightAns++;

  if (this.isRight(this.roomUser, this.roomText)) rightAns++;

  const allAnswersFilled = [
    this.answers.que4,
    this.answers.que5,
    this.answers.que6,
  ].every(ans => ans.year && ans.month && ans.day && ans.time);

  this.wrongUserAnswers = this.userAnswers.map(
    (ans, i) => this.isWrong(ans, this.userInfo[i])
  );

  this.wrongTimes.que4 = this.answers.que4.time !== "13:00";
  this.wrongTimes.que5 = this.answers.que5.time !== "13:00";
  this.wrongTimes.que6 = this.answers.que6.time !== "07:00";

  this.wrongReason = this.isWrong(this.reasonAnswer, this.reason);
  this.wrongRoom = this.isWrong(this.roomUser, this.roomText);

  const correctDate1 = { year: "2025", month: "06", day: "05" };
  const correctDate2 = { year: "2025", month: "06", day: "06" };

  const q4 = this.answers.que4;
  const q5 = this.answers.que5;
  const q6 = this.answers.que6;

  this.wrongDates.que4 = !(
    q4.year === correctDate1.year &&
    q4.month === correctDate1.month &&
    q4.day === correctDate1.day
  );
  this.wrongDates.que5 = !(
    q5.year === correctDate1.year &&
    q5.month === correctDate1.month &&
    q5.day === correctDate1.day
  );
  this.wrongDates.que6 = !(
    q6.year === correctDate2.year &&
    q6.month === correctDate2.month &&
    q6.day === correctDate2.day
  );

  if (
    !this.wrongDates.que4 &&
    !this.wrongDates.que5 &&
    !this.wrongDates.que6
  ) {
    rightAns++;
  }

  this.$emit("saveName", this.firstName);

  if (rightAns === 7) {
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
    // nextDoc() {
    //   if (this.debugMode) {
    //     this.$emit("next-doc");
    //     return;
    //   }
    //   let rightAns = 0;

    //   if (!this.signed && !this.chosen) {
    //     alert("וודאו שהקפתם את אפשרות הנכונה וחתמתם");
    //   } else {
    //     rightAns++; // ✅ מוסיפים ניקוד רק כשגם חתום וגם נבחר מסמך
    //   }

    //   const allCorrect = this.userAnswers.every(
    //     (ans, i) =>
    //       this.normalizeText(ans) === this.normalizeText(this.userInfo[i])
    //   );

    //   if (allCorrect) {
    //     rightAns++;
    //   }

    //   if (this.reasonAnswer.trim() === this.reason) rightAns++;

    //   if (
    //     this.answers.que4.time === "13:00" &&
    //     this.answers.que5.time === "13:00"
    //   )
    //     rightAns++;
    //   if (this.answers.que6.time === "07:00") rightAns++;
    //   if (this.roomUser.trim() === this.roomText) rightAns++;

    //   const allAnswersFilled = [
    //     this.answers.que4,
    //     this.answers.que5,
    //     this.answers.que6,
    //   ].every((ans) => ans.year && ans.month && ans.day && ans.time);

    //   this.wrongUserAnswers = this.userAnswers.map((ans, i) => {
    //     return this.normalizeText(ans) !== this.normalizeText(this.userInfo[i]);
    //   });
    //   this.wrongTimes.que4 = this.answers.que4.time !== "13:00";
    //   this.wrongTimes.que5 = this.answers.que5.time !== "13:00";
    //   this.wrongTimes.que6 = this.answers.que6.time !== "07:00";

    //   this.wrongReason = this.reasonAnswer.trim() !== this.reason;
    //   this.wrongRoom = this.roomUser.trim() !== this.roomText;

    //   const correctDate1 = { year: "2025", month: "06", day: "05" };
    //   const correctDate2 = { year: "2025", month: "06", day: "06" };

    //   const q4 = this.answers.que4;
    //   const q5 = this.answers.que5;
    //   const q6 = this.answers.que6;

    //   this.wrongDates.que4 = !(
    //     q4.year === correctDate1.year &&
    //     q4.month === correctDate1.month &&
    //     q4.day === correctDate1.day
    //   );
    //   this.wrongDates.que5 = !(
    //     q5.year === correctDate1.year &&
    //     q5.month === correctDate1.month &&
    //     q5.day === correctDate1.day
    //   );
    //   this.wrongDates.que6 = !(
    //     q6.year === correctDate2.year &&
    //     q6.month === correctDate2.month &&
    //     q6.day === correctDate2.day
    //   );

    //   // ✅ הוספת ציון רק אם כל התאריכים תקינים
    //   if (
    //     !this.wrongDates.que4 &&
    //     !this.wrongDates.que5 &&
    //     !this.wrongDates.que6
    //   ) {
    //     rightAns++;
    //   }
    //   // שמירת השם
    //   this.$emit("saveName", this.firstName);
    //   // בדיקה סופית
    //   if (rightAns === 7) {
    //     this.$emit("result", "right");
    //     setTimeout(() => {
    //       this.$emit("result", "");
    //       this.$emit("next-doc");
    //     }, 2200);
    //   } else {
    //     this.$emit("result", "wrong");
    //     setTimeout(() => {
    //       this.$emit("result", "");
    //     }, 2200);
    //   }
    // },

    // שעות
    generateTimeOptions() {
      const times = [];
      for (let h = 0; h < 24; h++) {
        for (let m = 0; m < 60; m += 60) {
          const hour = h.toString().padStart(2, "0");
          const minute = m.toString().padStart(2, "0");
          times.push(`${hour}:${minute}`);
        }
      }
      this.timeOptions = times;
    },

    years() {
      const year = [];
      for (let y = 1980; y < 2026; y++) {
        year.push(y.toString());
      }
      this.yearsArr = year;
    },

    days() {
      const days = [];
      for (let d = 1; d <= 31; d++) {
        days.push(d.toString().padStart(2, "0"));
      }
      this.dayArr = days;
    },

    months() {
      const month = [];
      for (let m = 1; m <= 12; m++) {
        month.push(m.toString().padStart(2, "0"));
      }
      this.monthArr = month;
    },

    // פרטי החייל או העוצר
    choose(event) {
      const currentId = event.target.id;
      if (currentId === "solider") {
        this.chosen = "solider";
      }
    },
    sign() {
      this.signed = true;
    },

    // פונקציה לבדיקה אם המחרוזת מכילה מספר
    containsNumber(str) {
      return /\d/.test(str);
    },
    // בודק אם זה מספר ובדיוק 7 ספרות

    checkInput(value) {
      const isNumber = !isNaN(value);
      const isSevenDigits = /^\d{7}$/.test(value);
      return isNumber && isSevenDigits;
    },
    openInfo() {
      if (this.doc === 0) {
        this.doc = 1;
      } else {
        this.doc = 0;
      }
      this.isInfoOpen = !this.isInfoOpen;
    },
  },
};
</script>

<style scoped>
.document1 {
  width: 40rem;
  height: 45rem;
  background-image: url("@/assets/media/part1documents/arrestReport.svg");
  background-size: 100% 100%;
  background-repeat: no-repeat;
  overflow: hidden;
}
.result {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 2;
}
.marking2 {
  position: relative;
  top: 8.6rem;
  right: 15.2rem;
  width: 3.2rem;
  height: 1rem;
  border: solid 2px rgb(0, 0, 0);
  border-radius: 100%;
  opacity: 0;
  cursor: pointer;
}
.signature {
  width: 3rem;
  position: relative;
  top: -17rem;
  right: 28.5rem;
  cursor: pointer;
  opacity: 0;
}
.chosen {
  opacity: 1;
}
.que1 {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: -1rem;
}
.input {
  position: relative;
  margin-top: 11.5rem;
  right: 9.5rem;
  width: 2.7rem;
  /* border: solid 2px; */

  border-radius: 5px;
  font-size: 0.7rem;
}
.que2 {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: -6.5rem;
}
.que3 {
  display: flex;
  flex-direction: row;
  align-items: center;
}
.que4 {
  display: flex;
  flex-direction: row;
  align-items: center;
}
.que4-text {
  display: flex;
  flex-direction: row;
  align-items: center;
}
.input3 {
  width: 20rem;
  position: relative;
  margin-top: 2rem;
  right: 10rem;
  /* border: none; */
  border-radius: 5px;
}
.input4 {
  position: relative;
  margin-top: 2.5rem;
  right: 19.4rem;
  width: 2rem;
  /* height: 1rem; */
  border-radius: 5px;
}
#time4 {
  margin-left: 0.8rem;
  width: 2.3rem;
}
#text4 {
  position: relative;
  top: -11.3rem;
  right: 22rem;
  width: 3rem;
}
.input5 {
  position: relative;
  top: -10.5rem;
  right: 8rem;
  width: 2rem;
  /* border: solid 2px; */
  border-radius: 5px;
}
.input6 {
  position: relative;
  top: -14rem;
  right: 18rem;
  width: 2rem;
  /* border: solid 2px; */
  border-radius: 5px;
}
#time5 {
  margin-right: 0.2rem;
  width: 2.3rem;
}
#time6 {
  margin-right: 0.2rem;
  width: 2.3rem;
}
.correct {
  border: 2px solid green;
  background-color: #e0ffe0;
}

.wrong {
  border: 2px solid red;
  background-color: #ffe0e0;
}
.button-next {
  position: absolute;
  bottom: 2rem;
  left: 7rem;
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
.container-details {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.details {
  width: 16rem;
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
  .input4 {
    margin-top: 2rem;
  }
  .input5 {
    margin-top: 2.3rem;
  }
  .signature {
    top: -16.5rem;
  }
  #text4 {
    top: -11.4rem;
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
    bottom: 45.8rem;
    left: 23rem;
  }
  .information {
    position: absolute;
    top: -7rem;
    right: 8rem;
  }
  .input {
    margin-top: 11.4rem;
    width: 2.55rem;
  }
}
@media (max-width: 870px) {
  .input4 {
    margin-top: 1.7rem;
  }
  .input5 {
    margin-top: 2rem;
  }
  .input6 {
    margin-top: 2.2rem;
  }
  #text4 {
    top: -11.4rem;
  }
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
    right: 19.5rem;
  }
  .input {
    margin-top: 11.4rem;
    width: 2.45rem;
  }
  .input4 {
    margin-top: 1.4rem;
  }
  .input5 {
    margin-top: 1.8rem;
  }
  .input6 {
    top: -13.3rem;
  }
  #text4 {
    top: -11.4rem;
  }
  .signature {
    top: 15rem;
  }
  .detailBtn {
    right: 23rem;
  }
  .infoBtn {
    left: 20rem;
  }
}
@media (max-width: 420px) {
  .que2 {
  margin-top: -7rem;
}
.input4 {
    margin-top: 1.6rem;
  }
}
.signature {
    top: -16.5rem;
  }
</style>
