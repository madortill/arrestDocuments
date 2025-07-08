<template>
  <div id="basic-documents">
    <document1 v-if="doc === 1" class="part1" @next-doc="nextDoc"></document1>
    <document2 v-if="doc === 2" class="part1" @backToTable="backToTable" ></document2>
    <div class="contaner-details">
      <p class="detailBtn" @click="isOpen = !isOpen">עזרה</p>
      <img
        v-show="isOpen"
        src="@/assets/media/part1documents/details.svg"
        alt="details"
        class="details"
      />
    </div>
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
      isOpen: false,
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
  background-image: url("@/assets/media/Artboard 2.png");
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
.container-details {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.details {
  width: 16rem;
  margin-top: 10rem;
  margin-right: 70rem;
}

.detailBtn {
  position: relative;
  height: 1rem;
  right: 65rem;
  top: 8rem;
  width: 5rem;
  z-index: 1;
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

</style>
