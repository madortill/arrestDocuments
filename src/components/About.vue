<template>
    <div id="about">
      <button class="aboutBtn" @click="openAbout">i</button>
      <Transition  name="fade"> 
        <div v-show="showAbout" class="div-about">
          <h3 class="list-text-about">מפתחת ראשית:</h3>
          <p class="list-text-about">רב"ט מאיה מרום</p>
          <h3 class="list-text-about">גרפיקה:</h3>
          <p class="list-text-about">סמל קריסטינה ברחטוב, רב"ט מאיה מרום</p>
          <h3 class="list-text-about">מומחות תוכן:</h3>
          <p class="list-text-about">סגן רעות שגיא, סגן יהב רייזל</p>
          <h3 class="list-text-about">רמ"ד טי"ל:</h3>
          <p class="list-text-about">רס"מ עדן בן חמו</p>
          <h3 class="list-text-about">גרסה:</h3>
          <p class="list-text-about">נובמבר 2025</p>
        </div>
      </Transition>
    </div>
  </template>
  
  <script>
  export default {
    name: "about",
    components: {
    },
    data() {
      return {
        showAbout: false,
        clickBtn: 0,
      };
    },
    methods: {
      openAbout() {
        if (this.clickBtn % 2 === 0) {
          this.showAbout = true;
        } else {
          this.showAbout = false;
        }
        this.clickBtn++;
      },
    },
  };
  </script>
  
  <style scoped>
  .aboutBtn {
    position: absolute;
    border: none;
    color: white;
    font-size: 1.6rem;
    transition: background-color 0.3s ease;
    background-color: #e10202;
    border-radius: 150px;
    width: 2rem;
    height: 2.2rem;
    cursor: pointer;
    left: 2.9%;
    top: 19%;
  }
  
  .aboutBtn:hover {
    background-color: #b90303;
  }
  .div-about {
    position: absolute;
    width: 12rem;
    /* height: rem; */
    left: 11%;
    top: 8%;
    font-family: "rubik";
    background: #fff;
    border-radius: 1rem;
    box-shadow: 0 15px 20px -20px rgba(0, 0, 0, 0.4);
    text-align: center;
    padding: 1rem;
    /* color: #0E2C8E; */
  }
  
  .list-text-about {
    transition: background-color 0.5s ease;
    margin: 5%;
  }
  .list-text-about:hover {
    background-color: #dbdbdb;
  }
  
  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.5s ease;
  }
  .fade-enter-from,
  .fade-leave-to {
    opacity: 0;
  }
  .fade-enter-to,
  .fade-leave-from {
    opacity: 1;
  }
  </style>
  