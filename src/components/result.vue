<template>
    <div id="result">
        <div v-if="resultFrom === 'right'" class="container">
            <p class="text right">כל הכבוד ענית נכון על כל השאלות!</p>
        </div>
        <div v-if="resultFrom === 'wrong'" class="container">
            <p class="text">יש שאלות שצריך לתקן...</p>
        </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "result",
    props: ['resultFrom'],
    components: {
    },
    data() {
      return {
      };
    },
    methods: {
    },
  };
  </script>
  
  <style scoped>
  #result {
    z-index: 8;
  }
  .container{
    width: 10rem;
    height: 10rem;
    background-color: #0e2c8e;
    overflow: hidden;
    text-align: center;
    padding: 1rem;
    border-radius: 2rem;
  }
  .text {
    font-family: "rubik";
    color: white;
    direction: rtl;
    position: relative;
    top: 1rem;
    right: 1.6rem;
    width: 7rem;
    font-size: 1.5rem;
  }
  .right {
    position: relative;
    top: 1rem;
    right: 1.2rem;
    width: 8rem;
  }
  </style>
  