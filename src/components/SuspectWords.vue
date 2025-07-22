<template>
  <div id="suspect-words">
    <div>
      <div class="bubble-img-container">
        <p class="text">{{ sentenceArr[currentSentence] }}</p>
        <img
          v-show="currentSentence > 0"
          src="@/assets/media/suspectWords/arrow.png"
          class="right-arrow"
          @click="currentSentence--"
          alt="arrow"
        />
        <img
          v-show="currentSentence < 3"
          src="@/assets/media/suspectWords/arrow.png"
          class="left-arrow"
          @click="add"
          alt="arrow"
        />
      </div>
      <img
        src="@/assets/media/suspectWords/discussion.png"
        class="discussion-img"
        alt="discussion"
      />
      <p class="continue-btn" :class="{'show' : showBtn}" @click="moveToDocs">למסמכים</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "SuspectWords",
  data() {
    return {
      sentenceArr: [
        "אני רוצה להגיד משהו בנוגע למעצר שלי, אני חושב שלא מגיע לי להיעצר כי אני מביע חרטה. ",
        "אני צריך חולצות, תחתונים ואת כדורי האלרגיה שלי",
        "אני רוצה לדבר עם העורך דין שלי סגן אלעד כהן.",
        "אני לא רוצה להודיע לאף אדם קרוב שאני עצור, אני מתבייש וגם אני לא רוצה שהשם שלי יתפרסם ויפגע.",
      ],
      currentSentence: 0,
      showBtn: false,
    };
  },

  methods: {
    add() {
        this.currentSentence++;
      if (this.currentSentence === 3) {
        this.showBtn = true;
      }
    },
    moveToDocs() {
        this.$emit('show-doc');
    },
  },
};
</script>

<style scoped>
#suspect-words {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.discussion-img {
  width: 80rem;
  height: 100vh;
  position: relative;
  top: -4.8rem;
}
.bubble-img-container {
  background-image: url("@/assets/media/suspectWords/talkBubble.png");
  background-size: 100% 100%;
  background-repeat: no-repeat;
  overflow: hidden;
  width: 22rem;
  height: 15rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  top: 14rem;
  right: 20rem;
  z-index: 2;
}
.bubble-img {
  position: relative;
  top: 10rem;
  right: 20rem;
  z-index: 2;
}
.text {
  width: 15rem;
  position: relative;
  top: 2.5rem;
  right: 1.5rem;
  text-align: center;
  font-family: "rubik";
}
.right-arrow {
  width: 2rem;
  position: absolute;
  top: 7.5rem;
  right: 5rem;
  cursor: pointer;
}
.left-arrow {
  width: 2rem;
  position: absolute;
  top: 7.5rem;
  right: 18rem;
  transform: rotate(178deg);
  cursor: pointer;
}
.continue-btn {
  font-family: "rubik";
  font-weight: bold;
  font-size: 1.3rem;
  background-color: #be0000;
  padding: 0.5rem;
  border-radius: 1rem;
  color: white;
  width: 7rem;
  text-align: center;
  position: relative;
  top: -12rem;
  right: 38rem;
  opacity: 0;
  pointer-events: none;
}
.continue-btn:hover {
  background-color: #d40000;
}
.show {
    opacity: 1;
    cursor: pointer;
    pointer-events: all;
}
</style>
