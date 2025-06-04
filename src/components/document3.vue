<template>
  <div id="document3">
    <input
      type="checkbox"
      class="checkBox"
      :class="{ 'checkbox-error': showCheckboxError }"
      v-model="isChecked"
    />
    <div
      class="mark"
      @click="choose"
      :class="{
        chosen: chosen,
      }"
    ></div>

    <div class="solider-unit-date">
      <input
        v-for="(answer, i) in userAnswers11"
        :key="i"
        :id="'input' + i"
        type="text"
        class="input1"
        :class="{ wrong: wrongInputs1[i] }"
        v-model="userAnswers11[i]"
      />
      <input
        type="text"
        v-model="selectedTime1"
        class="input2"
        :class="{ wrong: isTimeWrong }"
      />
    </div>
    <div class="solider-unit-details">
      <input
        v-for="(answer3, i) in userAnswers12"
        :key="i"
        :id="'input' + i"
        type="text"
        class="input3"
        :class="{
          wrong: wrongInputs12[i],
          'last-input3': i === userAnswers12.length - 1,
        }"
        v-model="userAnswers12[i]"
      />
    </div>

    <div class="public-officer-date">
      <input
        v-for="(answer, i) in userAnswers21"
        :key="i"
        :id="'input' + i"
        type="text"
        class="input12"
        :class="{ wrong: wrongInputs2[i] }"
        v-model="userAnswers21[i]"
      />
      <input
        type="text"
        v-model="selectedTime2"
        class="input22"
        :class="{ wrong: isTimeWrong2 }"
      />
    </div>
    <div class="public-officer-details">
      <input
        v-for="(answer3, i) in userAnswers22"
        :key="i"
        :id="'input' + i"
        type="text"
        class="input32"
        :class="{
          wrong: wrongInputs22[i],
          'last-input32': i === userAnswers22.length - 1,
        }"
        v-model="userAnswers22[i]"
      />
    </div>

    <div class="headquarters-date">
      <input
        v-for="(answer, i) in userAnswers31"
        :key="i"
        :id="'input' + i"
        type="text"
        class="input13"
        :class="{ wrong: wrongInputs3[i] }"
        v-model="userAnswers31[i]"
      />
      <input
        type="text"
        v-model="selectedTime3"
        class="input23"
        :class="{ wrong: isTimeWrong3 }"
      />
    </div>
    <div class="headquarters-details">
      <input
        v-for="(answer3, i) in userAnswers32"
        :key="i"
        :id="'input' + i"
        type="text"
        class="input33"
        :class="{
          wrong: wrongInputs32[i],
          'last-input3': i === userAnswers32.length - 1,
        }"
        v-model="userAnswers32[i]"
      />
    </div>

    <div class="escorts-date">
      <input
        v-for="(answer, i) in userAnswers41"
        :key="i"
        :id="'input' + i"
        type="text"
        class="input14"
        :class="{ wrong: wrongInputs4[i] }"
        v-model="userAnswers41[i]"
      />
      <input
        type="text"
        v-model="selectedTime4"
        class="input24"
        :class="{ wrong: isTimeWrong4 }"
      />
    </div>
    <div class="escorts-details">
      <input
        v-for="(answer3, i) in userAnswers42"
        :key="i"
        :id="'input' + i"
        type="text"
        class="input34"
        :class="{
          wrong: wrongInputs42[i],
          'last-input3': i === userAnswers42.length - 1,
        }"
        v-model="userAnswers42[i]"
      />
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

    <button @click="backToTable" class="back-btn" :class="{ 'disabled-btn': !areAllFieldsFilled() }"
    :disabled="!areAllFieldsFilled()">בדיקה</button>
  </div>
</template>

<script>
export default {
  name: "document3",
  components: {},
  data() {
    return {
      isChecked: false,
      showCheckboxError: false,
      chosen: false,
      signed: false,
      userAnswers11: Array(3).fill(""),
      userAnswers12: Array(4).fill(""),
      userAnswers21: Array(3).fill(""),
      userAnswers22: Array(2).fill(""),
      userAnswers31: Array(3).fill(""),
      userAnswers32: Array(4).fill(""),
      userAnswers41: Array(3).fill(""),
      userAnswers42: Array(4).fill(""),
      isChecked: false,
      selectedTime1: "",
      selectedTime2: "",
      selectedTime3: "",
      selectedTime4: "",
      selectedDate: ["25", "06", "05"],
      wrongInputs1: [],
      wrongInputs2: [],
      wrongInputs3: [],
      wrongInputs4: [],
      wrongInputs12: [false, false, false, false],
      wrongInputs22: [false, false],
      wrongInputs32: [false, false, false, false],
      wrongInputs42: [false, false, false, false],
      isTimeWrong: false,
      isTimeWrong2: false,
      isTimeWrong3: false,
      isTimeWrong4: false,
      soliderUnitArr: ['רס"ר', "מאור זגורי", "נגד מטבח", "0502265481"],
      publicOfficerArr: ['קפ"צ', "1111"],
      headquarters: ['סג"ם', "אריאל גיל", 'קמב"ץ', "0586695478"],
      escortsArr: ['סג"ם', "שובל מלכה", "קצין ליווים", "098972950"],
    };
  },
  methods: {
    // מקיף
    choose() {
      this.chosen = true;
    },
    // חותם
    sign() {
      this.signed = true;
    },

    areAllFieldsFilled() {
  return (
    this.signed &&
    this.chosen &&
    this.isChecked &&
    this.userAnswers11.every(val => val.trim() !== "") &&
    this.selectedTime1.trim() !== "" &&
    this.userAnswers12.every(val => val.trim() !== "") &&
    this.userAnswers21.every(val => val.trim() !== "") &&
    this.selectedTime2.trim() !== "" &&
    this.userAnswers22.every(val => val.trim() !== "") &&
    this.userAnswers31.every(val => val.trim() !== "") &&
    this.selectedTime3.trim() !== "" &&
    this.userAnswers32.every(val => val.trim() !== "") &&
    this.userAnswers41.every(val => val.trim() !== "") &&
    this.selectedTime4.trim() !== "" &&
    this.userAnswers42.every(val => val.trim() !== "")
  );
    },

    backToTable() {
      let rightAns = 0;

      if (this.isChecked) {
        rightAns++;
        this.showCheckboxError = false;
      } else {
        this.showCheckboxError = true;
      }
      //   שאלה 1
      const isDateCorrect = this.userAnswers11.every(
        (val, index) => val.trim() === this.selectedDate[index]
      );
      this.wrongInputs1 = this.userAnswers11.map(
        (val, index) => val.trim() !== this.selectedDate[index]
      );

      const isTimeCorrect = this.selectedTime1.trim() === "13:28";
      this.isTimeWrong = !isTimeCorrect;

      const isDetailsCorrect = this.userAnswers12.every(
        (val, index) => val.trim() === this.soliderUnitArr[index]
      );
      this.wrongInputs12 = this.userAnswers12.map(
        (val, index) => val.trim() !== this.soliderUnitArr[index]
      );

      if (isDateCorrect && isTimeCorrect && isDetailsCorrect) {
        rightAns++;
      }

      //   שאלה 2
      // בדיקת תאריך
      this.wrongInputs2 = this.userAnswers21.map(
        (val, index) => val.trim() !== this.selectedDate[index]
      );
      const isDateCorrect2 = this.wrongInputs2.every(
        (isWrong) => isWrong === false
      );

      // בדיקת שעה
      this.isTimeWrong2 = this.selectedTime2.trim() !== "13:18";
      const isTimeCorrect2 = !this.isTimeWrong2;

      // בדיקת פרטים
      this.wrongInputs22 = this.userAnswers22.map(
        (val, index) => val.trim() !== this.publicOfficerArr[index]
      );
      const isDetailsCorrect2 = this.wrongInputs22.every(
        (isWrong) => isWrong === false
      );

      // סיכום
      if (isDateCorrect2 && isTimeCorrect2 && isDetailsCorrect2) {
        rightAns++;
      }

      //   שאלה 3

      // בדיקת תאריך
      this.wrongInputs3 = this.userAnswers31.map(
        (val, index) => val.trim() !== this.selectedDate[index]
      );
      const isDateCorrect3 = this.wrongInputs3.every(
        (isWrong) => isWrong === false
      );

      // בדיקת שעה
      this.isTimeWrong3 = this.selectedTime3.trim() !== "13:22";
      const isTimeCorrect3 = !this.isTimeWrong3;

      // בדיקת פרטים
      this.wrongInputs32 = this.userAnswers32.map(
        (val, index) => val.trim() !== this.headquarters[index]
      );
      const isDetailsCorrect3 = this.wrongInputs32.every(
        (isWrong) => isWrong === false
      );

      // סיכום
      if (isDateCorrect3 && isTimeCorrect3 && isDetailsCorrect3) {
        rightAns++;
      }

      //   שאלה 4
      // בדיקת תאריך
      this.wrongInputs4 = this.userAnswers41.map(
        (val, index) => val.trim() !== this.selectedDate[index]
      );
      const isDateCorrect4 = this.wrongInputs4.every(
        (isWrong) => isWrong === false
      );

      // בדיקת שעה
      this.isTimeWrong4 = this.selectedTime4.trim() !== "13:30";
      const isTimeCorrect4 = !this.isTimeWrong4;

      // בדיקת פרטים
      this.wrongInputs42 = this.userAnswers42.map(
        (val, index) => val.trim() !== this.escortsArr[index]
      );
      const isDetailsCorrect4 = this.wrongInputs42.every(
        (isWrong) => isWrong === false
      );

      // סיכום
      if (isDateCorrect4 && isTimeCorrect4 && isDetailsCorrect4) {
        rightAns++;
      }

      if(rightAns === 6) {
        alert("הכל נכון כל הכבוד!");
        this.$emit("backToTable");
      } else {
        alert("קיימות תשובות שגויות");
      }
    },
  },
};
</script>

<style scoped>
#document3 {
  width: 40rem;
  height: 43rem;
  background-image: url("@/assets/media/part2documents/phoneDocument.svg");
  background-size: 100% 100%;
  background-repeat: no-repeat;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.checkBox {
  margin-top: 4.6rem;
  margin-left: 20.2rem;
  cursor: pointer;
  accent-color: #474747;
}
.mark {
  width: 1.2rem;
  height: 1rem;
  margin-top: -0.9rem;
  margin-left: 2.2rem;
  border: solid 2px #474747;
  border-radius: 20rem;
  cursor: pointer;
  opacity: 0;
}
.signature {
  width: 4rem;
  position: relative;
  top: 5rem;
  right: 7rem;
  cursor: pointer;
  opacity: 0;
}
.chosen {
  opacity: 1;
}
.solider-unit-date {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 1.8rem;
  margin-right: -9rem;
  gap: 0.3rem;
}
.input1 {
  width: 0.8rem;
}
.input2 {
  position: relative;
  width: 2.5rem;
  right: 1.6rem;
}
.solider-unit-details {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 0.1rem;
  margin-right: -2rem;
  gap: 0.5rem;
}
.input3 {
  width: 3rem;
}
/* שאלה 2 */
.public-officer-date {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 3.8rem;
  margin-right: -8.6rem;
  gap: 0.3rem;
}
.input12 {
  width: 0.8rem;
}
.input22 {
  position: relative;
  width: 2.5rem;
  right: 1.6rem;
}
.public-officer-details {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 0.2rem;
  margin-right: -1.5rem;
  gap: 0.5rem;
  transform: rotate(-0.5deg);
}
.input32 {
  width: 3rem;
}
.last-input32 {
  margin-right: 11rem;
  width: 4rem;
}

/* שאלה 3 */
.headquarters-date {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 3.8rem;
  margin-right: -8.6rem;
  gap: 0.3rem;
}
.input13 {
  width: 0.8rem;
}
.input23 {
  position: relative;
  width: 2.5rem;
  right: 1.6rem;
}
.headquarters-details {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 0.2rem;
  margin-right: -2.5rem;
  gap: 0.5rem;
  transform: rotate(-0.5deg);
}
.input33 {
  width: 3rem;
}

/* שאלה 4 */
.escorts-date {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 3.8rem;
  margin-right: -8.6rem;
  gap: 0.3rem;
}
.input14 {
  width: 0.8rem;
}
.input24 {
  position: relative;
  width: 2.5rem;
  right: 1.6rem;
}
.escorts-details {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 0.2rem;
  margin-right: -2.5rem;
  gap: 0.5rem;
  transform: rotate(-0.5deg);
}
.input34 {
  width: 3rem;
}
.last-input3 {
  margin-right: 3.2rem;
  width: 4rem;
}
.wrong {
  border: 2px solid red;
  background-color: #ffe5e5;
}
.checkbox-error {
  outline: 2px solid red;
  box-shadow: 0 0 5px red;
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
