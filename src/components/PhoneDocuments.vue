<template>
  <div id="phone-documents">
    <result class="result" :resultFrom="propsResult" />
    <div v-if="propsResult != ''" class="blackDiv"></div>
    <document3 class="part1" @result="showResult" @backToTable="backToTable"></document3>
  </div>
</template>

<script>
import document3 from "@/components/document3.vue";
import result from "./result.vue";
export default {
  name: "phone-documents",
  components: {
    document3,
    result
  },
  data() {
    return {
      propsResult: '',
    };
  },
  methods: {
    backToTable() {
      this.$emit("backToTable", "cop");
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
#phone-documents {
  background-image: url("@/assets/media/backGround.png");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  min-height: 100vh; /* במקום height */
  overflow-y: auto; /* גלילה אנכית */
  position: relative; /* כדי לאפשר מיקום יחסי של תוכן */
}
.part1 {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-58%, -50%);
  margin-right: 5rem;
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
