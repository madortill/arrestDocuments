<template>
  <div id="interrogation-room" :class="{ clicked: isBrown }">
    <instructions
      v-if="showInstruction"
      @close="closeInstruction"
    ></instructions>
    <basic-documents
      v-if="page === 1"
      @backToTable="showTable"
      @saveName="saveName"
    ></basic-documents>
    <phone-documents
      v-if="page === 2"
      @backToTable="showTable"
    ></phone-documents>
    <suspect-documents
      v-if="page === 3"
      @end-practice="endInvestigation"
    ></suspect-documents>
    <div v-show="page === 0" class="table-container">
      <Table
        v-show="!isClick"
        class="table"
        @zoom="zoomDocuments"
        @move="moveToDoc"
      ></Table>
      <img
        src="@/assets/media/interrogationRoom/documents.png"
        v-show="isClick"
        class="documents"
        @click="moveToDoc"
        alt="documents"
      />
    </div>
    <div v-if="showInstruction" class="blackDiv"></div>
  </div>
</template>

<script>
import instructions from "@/components/instructions.vue";
import Table from "@/components/Table.vue";
import BasicDocuments from "@/components/BasicDocuments.vue";
import PhoneDocuments from "@/components/PhoneDocuments.vue";
import SuspectDocuments from "@/components/SuspectDocuments.vue";

export default {
  name: "interrogation-room",
  components: {
    Table,
    BasicDocuments,
    PhoneDocuments,
    instructions,
    SuspectDocuments,
  },
  data() {
    return {
      isClick: false,
      isBrown: false,
      page: 0
      ,
      showInstruction: true,
      object: "documents",
    };
  },
  methods: {
    closeInstruction() {
      this.showInstruction = false;
    },
    zoomDocuments() {
      this.isClick = true;
      this.isBrown = true;
    },
    moveToDoc() {
      if (this.object === "documents") {
        this.page = 1;
      } else if (this.object === "phone") {
        this.page = 2;
      } else {
        this.page = 3;
      }
    },
    showTable(item) {
      this.page = 0;
      this.isClick = false;
      this.isBrown = false;
      this.object = item;
    },
    endInvestigation() {
      this.$emit("end-practice");
    },
    saveName(theName) {
      this.$emit("saveName", theName);
    },
  },
};
</script>

<style scoped>
#interrogation-room {
  position: relative;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}
.clicked {
  background-image: url("@/assets/media/backGround.png");
  background-size: 100vw 100vh;
  height: 100vh;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  overflow: hidden;
}
.table-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.table {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 2;
}
.documents {
  margin-top: 20rem;
  width: 5rem;
  cursor: pointer;
  animation: zoom 1.5s 0.5s forwards;
}
@keyframes zoom {
  0% {
    margin-top: 20rem;
    width: 5rem;
  }
  100% {
    margin-top: 13rem;
    width: 35rem;
  }
}
@-webkit-keyframes zoom {
  0% {
    margin-top: 20rem;
    width: 5rem;
  }
  100% {
    margin-top: 17rem;
    width: 28rem;
  }
}
@keyframes zoom1 {
  0% {
    margin-top: 20rem;
    width: 5rem;
  }
  100% {
    margin-top: 23rem;
    width: 28rem;
  }
}
@-webkit-keyframes zoom1 {
  0% {
    margin-top: 20rem;
    width: 5rem;
  }
  100% {
    margin-top: 13rem;
    width: 28rem;
  }
}
.blackDiv {
  width: 100vw;
  height: 100vh;
  position: absolute;
  z-index: 2;
  background-color: rgba(0, 0, 0, 0.623);
}
@media (max-width: 450px) {
  .table {
    width: 35rem;
  }
  .documents {
    animation: zoom1 1.5s 0.5s forwards;
  }
}
</style>
