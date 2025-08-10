<template>
  <div id="document6">
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
    <div class="contaner-details">
      <p class="detailBtn" @click="isOpen = !isOpen">{{ isOpen ? 'סגירה' : 'פרטים' }}</p>
      <details-box v-show="isOpen" :note="6" class="details"></details-box>
    </div>
    <img src="@/assets/media/part3documents/endBtn.png" @click="backToMap"
      class="back-btn"
      :class="{ 'disabled-btn': !debugMode && !areAllFieldsFilled() }"
      :disabled="!debugMode && !areAllFieldsFilled()" alt="btn">
    <!-- <button
      @click="backToMap"
      class="back-btn"
      :class="{ 'disabled-btn': !debugMode && !areAllFieldsFilled() }"
      :disabled="!debugMode && !areAllFieldsFilled()"
    >
      לסיום הלומדה!
    </button> -->
    <button class="infoBtn" @click="openInfo">{{ isInfoOpen ? 'סגירה' : 'דגשים למילוי' }}</button>
    <information :docNum="doc" class="information"></information>
    <img src="@/assets/media/part3documents/talk.png" class="conversion-btn" @click="backToDetails" alt="talk">
  </div>
</template>

<script>
import Information from "./Information.vue";
import DetailsBox from "./DetailsBox.vue";
export default {
  name: "document6",
  components: {
    Information,
    DetailsBox
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
      debugMode: true,
      doc: 0,
      DOC_NUM: 3,
      isOpen: false,
      isInfoOpen: false, 
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
        this.$emit("end-practice");
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
      if (allCorrect1) {
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
        this.$emit("result", "right");
        setTimeout(() => {
          this.$emit("result", "");
          this.$emit("end-practice");
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
        this.doc = 6;
      } else {
        this.doc = 0;
      }
      this.isInfoOpen = !this.isInfoOpen;
    },
    backToDetails() {
      this.$emit('to-details', this.DOC_NUM);
    }
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
  bottom: 0.5rem;
  left: 5.5rem;
  width: 6rem;
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
.result {
  z-index: 5;
}
.conversion-btn {
  width: 5rem;
  text-align: center;
  position: relative;
  top:11rem;
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
@media (max-width: 1200px) {
  .input1 {
    height: 0.8rem;
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
}
@media (max-width: 870px) {
  .information {
    right: 13rem;
  }
  .details {
    right: 25rem;
  }
  .signature {
    top: 17rem;
  }
}
@media (max-width: 610px) {
  .information {
    right: 16rem;
  }
  .details {
    right: 20.8rem;
  }
  .detailBtn {
    right: 22rem;
  }
  .infoBtn {
    left: 20rem;
  }
  .details2 {
  position: relative;
  top: -0.3rem;
}
}
</style>
