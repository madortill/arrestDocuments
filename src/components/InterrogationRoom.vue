<template>
    <div id="interrogation-room" :class="{'clicked' : isClick}">
        <basic-documents v-if="page === 1" @backToTable="showTable"></basic-documents>
        <phone-documents v-if="page === 2"></phone-documents>
      <div v-show="page === 0" class="table-container">
        <Table v-show="!isClick" class="table" @zoom="zoomDocuments" @phone="moveToDoc"></Table>
        <img src="@/assets/media/interrogationRoom/documents.svg" v-show="isClick" class="documents" @click="moveToDoc" alt="documents">
      </div>
    
      
    </div>
  </template>
  
  <script>
  import Table from '@/components/Table.vue';
  import BasicDocuments from '@/components/BasicDocuments.vue';
  import PhoneDocuments from '@/components/PhoneDocuments.vue';
  
  export default {
    name: "interrogation-room",
    components: {
      Table,
      BasicDocuments,
      PhoneDocuments
    },
    data() {
      return {
        isClick: false,
        page: 0,
        object: 'phone',
      };
    },
    methods: {
     zoomDocuments() {
        this.isClick = true;
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
    background-color: #846363;
  }
  .table-container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .table {
    margin-top: -2rem;
  }
  .documents {
    margin-top: 17rem;
    width: 8rem;
    cursor: pointer;
    animation: zoom 1.5s 0.5s forwards;
  }
  @keyframes zoom {
    0% {
        margin-top: 17rem;
        width: 8rem;
    }
    100% {
        width: 24rem;
        margin-top: 8rem;
    }
}
  @-webkit-keyframes zoom {
    0% {
        margin-top: 17rem;
        width: 8rem;
    }
    100% {
        width: 24rem;
        margin-top: 8rem;
    }
  }
  </style>
  
