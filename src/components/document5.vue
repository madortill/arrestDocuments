<template>
  <div id="document5">
    <div class="que1-details">
      <input
        v-for="(answer, i) in userAnswers"
        :key="i"
        :id="'input' + i"
        type="text"
        class="input1"
        :class="{ 'last-input1': i === userAnswers.length - 1 }"
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
        v-model="userAnswers1[i]"
      />
    </div>
    <div class="check-boxes">
      <input
        v-for="(answer, i) in checkBoxes1"
        :key="i"
        type="checkbox"
        class="check-box"
        :id="'check' + i"
        :value="answer"
      />
      <input
        v-for="(answer, i) in checkBoxes2"
        :key="i"
        type="checkbox"
        class="check-box"
        :id="'check' + i"
        :value="answer"
      />
    </div>
    <button class="back-btn">לעמוד הבא</button>
  </div>
</template>

<script>
export default {
  name: "document5",
  components: {},
  data() {
    return {
      userAnswers: Array(4).fill(""),
      userAnswers1: Array(3).fill(""),
      checkBoxes1: Array(2).fill(""),
      checkBoxes2: Array(3).fill(""),
      isChecked: [],
      showError: false,
    };
  },
  methods: {},
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
  gap: 1.2rem;
}
.input1 {
  position: relative;
  width: 2.5rem;
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
  margin-top: 0.9rem;
  margin-right: 16rem;
  gap: 0.6rem;
}
.check-box {
    accent-color: #474747;

}
#check0 {
    accent-color: #c40000;
}
#check1 {
    accent-color: #c40000;
}
#check4 {
    accent-color: #c40000;
}

</style>
