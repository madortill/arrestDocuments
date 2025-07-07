<template>
    <div id="end-screen">
        <p class="end">סיימת!!!</p>
        <button @click="startAgain">לתרגל שוב!</button>
    </div>

</template>

<script>
export default {
  name: "end-screen",
  data() {
     return{

     };
  },
  methods: {
    startAgain() {
        this.$emit("start-over");
    }
  }
};
</script>

<style scoped>
.end {
    color: brown;
    font-size: 5rem;
}

</style>
