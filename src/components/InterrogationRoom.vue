<template>
    <div id="interrogation-room" :class="{'clicked' : isBrown}">
      <instructions></instructions>
        <basic-documents v-if="page === 1" @backToTable="showTable"></basic-documents>
        <phone-documents v-if="page === 2" @backToTable="showTable"></phone-documents>
        <suspect-documents v-if="page === 3"></suspect-documents>
      <div v-show="page === 0" class="table-container">
        <Table v-show="!isClick" class="table" @zoom="zoomDocuments" @move="moveToDoc"></Table>
        <img src="@/assets/media/interrogationRoom/papers.svg" v-show="isClick" class="documents" @click="moveToDoc" alt="documents">
      </div>
    
      
    </div>
  </template>
  
  <script>
  import instructions from '@/components/instructions.vue';
  import Table from '@/components/Table.vue';
  import BasicDocuments from '@/components/BasicDocuments.vue';
  import PhoneDocuments from '@/components/PhoneDocuments.vue';
  import SuspectDocuments from '@/components/SuspectDocuments.vue';
  
  export default {
    name: "interrogation-room",
    components: {
      Table,
      BasicDocuments,
      PhoneDocuments,
      instructions,
      SuspectDocuments
    },
    data() {
      return {
        isClick: false,
        isBrown: false,
        page: 3,
        object: 'documents',
      };
    },
    methods: {
     zoomDocuments() {
        this.isClick = true;
        this.isBrown = true;
     },
     moveToDoc() {
      if(this.object === "documents") {
        this.page = 1;
      } else if(this.object === "phone") {
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
     }
    },
  };
  </script>
  
  <style scoped>
  #interrogation-room {
    width: 100%;
    height: 100%;
  }
  .clicked {
    background-color: #7B736E;
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
  </style>
  
