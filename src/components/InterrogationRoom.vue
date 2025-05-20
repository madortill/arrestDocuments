<template>
    <div id="interrogation-room" :class="{'clicked' : isClick}">
        <basic-documents v-if="page === 1"></basic-documents>
      <div v-if="page === 0" class="table-container">
        <Table v-show="!isClick" class="table" @zoom="zoomDocuments"></Table>
        <img src="@/assets/media/interrogationRoom/documents.svg" v-show="isClick" class="documents" @click="page = 1" alt="documents">
      </div>
    
      
    </div>
  </template>
  
  <script>
  import Table from '@/components/Table.vue';
  import BasicDocuments from '@/components/BasicDocuments.vue';
  
  export default {
    name: "interrogation-room",
    components: {
      Table,
      BasicDocuments
    },
    data() {
      return {
        isClick: false,
        page: 0,
      };
    },
    methods: {
     zoomDocuments() {
        this.isClick = true;
     },
     moveToDocuments() {

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
  
