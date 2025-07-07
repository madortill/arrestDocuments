<template>
    <div id="suspect-documents" class="background">
      
        <document4 v-show="doc === 1" @next-doc="doc = 2" class="part1"></document4>
        <document5 v-show="doc === 2"  @next-doc="doc = 3" class="part1"></document5>
        <document6 v-show="doc === 3" class="part1" @result="showResult" @end-practice="endInvestigation"></document6>
    </div>

</template>

<script>
import document4 from "@/components/document4.vue";
import document5 from "@/components/document5.vue";
import document6 from "@/components/document6.vue";
export default {
  name: "suspect-documents",
  components: {
    document4,
    document5,
    document6,
  },
  data() {
    return {
      doc: 1,
      result: false,
  };
},
  methods: {
    endInvestigation() {
        this.$emit("end-practice");
    },
    showResult(par) {
      this.result = par;
    }
  },
};
</script>

<style scoped>
#suspect-documents {
  width: 100%;
  height: 100%;
  background-color: #7B736E;
  overflow: hidden;
}
 .part1 {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 2;
}

</style>
