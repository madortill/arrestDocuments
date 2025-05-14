<template>
    <div id="suspect-info">
        <div class="container">
            <!-- <p>cfhcnhg</p> -->
            <img src="@/assets/media/suspectInfo/computer.svg" alt="computer" class="computer">
            <img src="@/assets/media/suspectInfo/suspect.svg" alt="computer" class="suspect">
            <p class="continue-btn" @click="toInterrogation">הבא</p>

        </div>
        
    </div>

</template>

<script>
export default {
  name: "suspect-info",
  components: {
  },
  data() {
     
  },
  methods: {
    toInterrogation () {
        this.$emit("next");
    }
  }
}
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 4rem;
  /* border: solid; */
}
.computer {
    /* width: 47rem; */
    align-items: center;
    margin-top: 3rem;
    margin-left: 30rem;
}
.suspect {
    margin-top: -30rem;
    margin-right: 40rem;
}
.continue-btn {
    font-family: "rubik";
    font-weight: bold;
    font-size: 1.5rem;
    background-color: #BE0000;
    padding: 1rem 2rem;
    border-radius: 1rem;
    margin-right: 70rem;
    cursor: pointer;
}
.continue-btn:hover {
    background-color: #d40000;
}
@media (max-width: 1444px) {
    .computer {
    width: 40rem;
    align-items: center;
    margin-left: 18rem;
}
.suspect {
    margin-right: 47rem;
    width: 10rem;
}
.continue-btn {
    margin-right: 50rem;
    margin-top: 5rem;
}

/* @media (max-width: 940px) {

} */
}

</style>
