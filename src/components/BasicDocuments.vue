<template>
  <div id="basic-documents">
    <document1 v-if="doc === 1" class="part1" @next-doc="nextDoc"></document1>
    <document2 v-if="doc === 2" class="part1" @backToTable="backToTable" ></document2>
  </div>
</template>

<script>
import document1 from "@/components/document1.vue";
import document2 from "@/components/document2.vue";
export default {
  name: "basic-documents",
  components: {
    document1,
    document2,
  },
  data() {
    return {
      doc: 1,
      
    };
  },
  methods: {
    nextDoc() {
    this.doc = 2;
  },
  backToTable() {
    this.$emit("backToTable", "phone");
  }

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


</style>
