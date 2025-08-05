<template>
  <div id="basic-documents">
    <result class="result" :resultFrom="propsResult" />
    <div v-if="propsResult != ''" class="blackDiv"></div>
    <document1 v-if="doc === 1" class="part1" @result="showResult" @next-doc="nextDoc" @saveName="saveName"></document1>
    <document2 v-if="doc === 2" class="part1" @result="showResult" @backToTable="backToTable" ></document2>
  </div>
</template>

<script>
import document1 from "@/components/document1.vue";
import document2 from "@/components/document2.vue";
import result from "./result.vue";
export default {
  name: "basic-documents",
  components: {
    document1,
    document2,
    result
  },
  data() {
    return {
      doc: 1,
      propsResult: '',
      
    };
  },
  methods: {
    nextDoc() {
    this.doc = 2;
  },
  backToTable() {
    this.$emit("backToTable", "phone");
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
    saveName(theName) {
      this.$emit("saveName", theName);
    },

  },
};
</script>

<style scoped>
#basic-documents {
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
