<template>
    <div id="open-screen">
        <div class="container">
            <notebook @start="nextPage" class="notebook"></notebook>
            <!-- <div class="noteBookContainer">
                <img src="@/assets/media/openingPage/noteBook.svg" alt="">
            </div> -->
            <!-- <p class="startBtn">לחצו כדי להתחיל לחקור!</p> -->
        </div>
        
    </div>

</template>

<script>
import Notebook from '@/components/Notebook.vue';
export default {
  name: "open-screen",
  components: {
    Notebook
  },
  data() {
     
  },
  methods: {
    nextPage () {
        this.$emit("start");
    }
  }
}
</script>

<style scoped>

.container {
    display: flex;
    flex-direction: column;
    align-items: center;
}
.title {
    font-family: "abraham";
    font-size: 2rem;
    color: white;

}
.noteBookContainer {
    flex-direction: column;
    align-items: center;
}
.notebook {
    margin-top: 7rem;
}
/* @media (max-width: 1444px) {
    note {
        width: ;
    }
} */
/* @media (max-width: 940px) {
    .notebook {
        width: 30rem;
        margin-top: 5.5rem;
    }
}
@media (max-width: 540px) {
    .notebook {
        width: 25rem;
        margin-top: 5.5rem;
    }
}
@media (max-width: 400px) {
    .notebook {
        width: 20rem;
        margin-top: 1rem;
    }
} */
</style>
