<template>
    <div id="document3">
        <input type="checkbox" class="checkBox">
        <div class="mark" @click="choose"
        :class="{
          chosen: chosen,
        }">

        </div>
    </div>

</template>

<script>

export default {
  name: "document3",
  components: {
  },
  data() {
    return {
        chosen: false,
  };
},
  methods: {
   choose() {
    this.chosen = true;
   }
  },

};
</script>


<style scoped>
 #document3 {
  width: 40rem;
  height: 43rem;
  background-image: url("@/assets/media/part2documents/phoneDocument.svg");
  background-size: 100% 100%;
  background-repeat: no-repeat;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.checkBox {
    margin-top: 4.6rem;
    margin-left: 20.2rem;
    cursor: pointer;
    accent-color: #474747;
}
.mark {
    width: 1.2rem;
    height: 1rem;
    margin-top: -0.9rem;
    margin-left: 2.2rem;
    border: solid 2px #474747;
    border-radius: 20rem;
    cursor: pointer;
    opacity: 0;
}
.chosen {
    opacity: 1;
}
</style>
