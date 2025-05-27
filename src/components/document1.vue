<template>
  <div id="part1-documents">
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
          v-model="userInput11"
          @input="updateWrongCount"
          :class="userInput11 === '' ? '' : { wrong: !checkInput(userInput11) }"
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
          v-model="userInput12"
          :class="
            userInput12 === '' ? '' : { wrong: containsNumber(userInput12) }
          "
        />
        <input
          type="text"
          ref="4"
          class="input"
          v-model="userInput13"
          :class="
            userInput13 === '' ? '' : { wrong: containsNumber(userInput13) }
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
          v-model="userInput41"
          class="input"
          :class="
            userInput41 === '' ? '' : { wrong: containsNumber(userInput41) }
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
          'chosen': signed,
        }"
      />
    </div>

    <button @click="nextDoc" class="button-next">לעמוד הבא</button>

    <!-- <p class="detailBtn" @click="isOpen = !isOpen">פרטי העצור</p>
    <img
      v-show="isOpen"
      src="@/assets/media/part1documents/details.svg"
      alt="details"
      class="details"
    /> -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputs: [],
      reasonAnswer: "",
      roomUser: "",
      userAnswers: Array(7).fill(""),
      userInfo: ["8859963", 'רב"ט', "רייס", "נועם", "האוויר", 'בא"ח 21', "טבח"],
      page: 1,
      ranks: ["טוראי", 'רב"ט', "סמל", "סמ'ר"],
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
      reason: "הטרדה מינית ומעשה מגונה בכוח",
      roomText: 'מצח ב"ש',
      userInput11: "",
      userInput12: "",
      userInput13: "",
      userInput21: "",
      userInput22: "",
      userInput23: "",
      userInput41: "",
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
      return (
        this.userInput11.trim() !== "" &&
        this.selectedRan1k &&
        this.userInput12.trim() !== "" &&
        this.userInput13.trim() !== "" &&
        this.selectedForse1 &&
        this.userInput41.trim() !== "" &&
        this.reasonAnswer.trim() !== "" &&
        this.roomUser.trim() !== "" &&
        this.userAnswers.every((ans) => ans.trim() !== "") &&
        [this.answers.que4, this.answers.que5, this.answers.que6].every(
          (ans) => ans.year && ans.month && ans.day && ans.time
        )
      );
    },

    nextDoc() {
      let rightAns = 0;

  
  if (!this.signed && !this.chosen) {
    alert("וודאו שהקפתם את אפשרות הנכונה וחתמתם")
} else {
  rightAns++; // ✅ מוסיפים ניקוד רק כשגם חתום וגם נבחר מסמך
}
      const isValidID = this.checkInput(this.userInput11);
      const isValidName1 = !this.containsNumber(this.userInput12);
      const isValidName2 = !this.containsNumber(this.userInput13);
      const isValidRoom = !this.containsNumber(this.userInput41);
      const allFilled = this.validateAllFields();

      if (!allFilled) {
        alert("תמלאו את כל השדות כדי להמשיך.");
        return;
      }

      if (!isValidID || !isValidName1 || !isValidName2 || !isValidRoom) {
        alert("יש למלא את כל השדות בצורה תקינה לפני המשך.");
        return;
      }

      const allCorrect = this.userAnswers.every(
        (ans, i) => ans.trim() === this.userInfo[i]
      );

      if (allCorrect) {
        rightAns++;
      }

      if (this.reasonAnswer.trim() === this.reason) rightAns++;

      if (
        this.answers.que4.time === "13:00" &&
        this.answers.que5.time === "13:00"
      )
        rightAns++;
      if (this.answers.que6.time === "05:00") rightAns++;
      if (this.roomUser.trim() === this.roomText) rightAns++;

      const allAnswersFilled = [
        this.answers.que4,
        this.answers.que5,
        this.answers.que6,
      ].every((ans) => ans.year && ans.month && ans.day && ans.time);

      this.wrongUserAnswers = this.userAnswers.map((ans, i) => {
        return ans.trim() !== this.userInfo[i];
      });

      this.wrongTimes.que4 = this.answers.que4.time !== "13:00";
      this.wrongTimes.que5 = this.answers.que5.time !== "13:00";
      this.wrongTimes.que6 = this.answers.que6.time !== "05:00";

      this.wrongReason = this.reasonAnswer.trim() !== this.reason;
      this.wrongRoom = this.roomUser.trim() !== this.roomText;

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

      console.log(q4, correctDate1);

      // ✅ הוספת ציון רק אם כל התאריכים תקינים
      if (
        !this.wrongDates.que4 &&
        !this.wrongDates.que5 &&
        !this.wrongDates.que6
      ) {
        rightAns++;
      } else {
        console.log("לא נכון!!!");
      }
      // שלב 2: בדיקה של התאמת תאריכים
      if (rightAns === 7 && allAnswersFilled) {
        alert("כל הכבוד! מילאת את כל התשובות נכון!");
        this.$emit("next-doc");
      } else {
        alert("יש למלא את כל השדות ולוודא שכל התשובות נכונות.");
      }
    },

    // שעות
    generateTimeOptions() {
      const times = [];
      for (let h = 0; h < 24; h++) {
        for (let m = 0; m < 60; m += 5) {
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
      console.log(this.signed)
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
}
.document2 {
  width: 40rem;
  height: 43rem;
  background-image: url("@/assets/media/part1documents/explainRights.svg");
  background-size: 100% 100%;
  background-repeat: no-repeat;
}
.marking1 {
  position: relative;
  top: 8.6rem;
  right: 11.3rem;
  width: 2rem;
  height: 1rem;
  border: solid 2px rgb(0, 0, 0);
  border-radius: 100%;
  opacity: 0;
  cursor: pointer;
}
.marking2 {
  position: relative;
  top: 8.5rem;
  right: 11.5rem;
  width: 3rem;
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
/* @media (max-width: 1470px) {
    .input4 {
      margin-top: 1.5rem;
    }
    #text4 {
      top: -11.4rem;
    }
}
@media (max-width: 1230px) {
    .input4 {
      margin-top: 1.1rem;
    }
    #text4 {
      top: -11.4rem;
    }
} */
</style>
