<template>
    <div id="open-screen">
        <div class="container">
            <p class="title">לומדת מילוי מסמכי מעצר</p>
            <notebook @start="nextPage"></notebook>
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
.startBtn {
    font-family: "dana";
    direction: rtl;
    font-size: 1.8rem;
    margin-top: -10rem;
    font-weight: bold;
    transform: rotate(5.6deg);
    
}
</style>
