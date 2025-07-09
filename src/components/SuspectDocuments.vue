<template>
    <div id="suspect-documents">
      <result class="result" :resultFrom="propsResult" />
      <div v-if="propsResult != ''" class="blackDiv"></div>
        <document4 v-show="doc === 1" @next-doc="doc = 2" @result="showResult" class="part1"></document4>
        <document5 v-show="doc === 2"  @next-doc="doc = 3" @result="showResult" class="part1"></document5>
        <document6 v-show="doc === 3" class="part1" @result="showResult" @end-practice="endInvestigation"></document6>
    </div>

</template>

<script>
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
    result
  },
  data() {
    return {
      doc: 1,
      propsResult: '',

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
    }
  },
};
</script>

<style scoped>
#suspect-documents {
  background-image: url("@/assets/media/backGround.png");
  background-size: 100vw 100vh;
  height: 100vh;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  overflow: hidden;
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

</style>
