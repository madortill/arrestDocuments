<template>
    <div id="suspect-documents" class="suspect-documents" :class="{'desk' : doc < 1}">
      <result class="result" :resultFrom="propsResult" />
      <div v-if="propsResult != ''" class="blackDiv"></div>
        <document4 v-show="doc === 1" @next-doc="doc = 2" @result="showResult" @to-details="whatDoc" class="part1"></document4>
        <document5 v-show="doc === 2"  @next-doc="doc = 3" @result="showResult" @to-details="whatDoc" class="part1"></document5>
        <document6 v-show="doc === 3" class="part1" @result="showResult" @to-details="whatDoc" @end-practice="endInvestigation"></document6>
        <suspect-words class="suspect-words" v-show="doc === 0" @show-doc="doc = backDoc"></suspect-words>
    </div>
    
</template>

<script>
import SuspectWords from "@/components/SuspectWords.vue";
import document4 from "@/components/document4.vue";
import document5 from "@/components/document5.vue";
import document6 from "@/components/document6.vue";
import result from "./result.vue";
export default {
  name: "suspect-documents",
  components: {
    document4,
    document5,
    document6,
    result,
    SuspectWords,

  },
  data() {
    return {
      doc: 0,
      propsResult: '',
      backDoc: 1,

  };
},
  methods: {
    endInvestigation() {
        this.$emit("end-practice");
    },
    showResult(par) {
      if(par === "right") {
        this.propsResult = "right"
      } else if (par === "wrong") {
        this.propsResult = "wrong"
      } else {
        this.propsResult = ""
      }
    },
    whatDoc(par) {
      this.doc = 0;
      this.backDoc = par;
    }
  },
};
</script>

<style scoped>
#suspect-documents {
  background-size: 100vw 100vh;
  height: 100vh;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  overflow: hidden;
}
.suspect-documents {
  background-image: url("@/assets/media/backGround.png");
}
.desk {
  background-image: url("@/assets/media/Artboard 2.svg");
}
 .part1 {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 2;
}
.blackDiv {
  width: 100vw;
  height: 100vh;
  position: absolute;
  z-index: 3;
  background-color: rgba(0, 0, 0, 0.623);
  pointer-events: none;
}

.suspect-words {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  /* z-index: 10; */
  z-index: 1;
}
.continue-btn {
  font-family: "rubik";
  font-weight: bold;
  font-size: 1.1rem;
  background-color: #be0000;
  padding: 0.5rem;
  border-radius: 1rem;
  color: white;
  width: 7rem;
  text-align: center;
  position: relative;
  top: 40rem;
  right: 10rem;
  cursor: pointer;
}
.continue-btn:hover {
  background-color: #d40000;
}
</style>
