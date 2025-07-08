<template>
    <div id="phone-documents">
        <document3 class="part1" @backToTable="backToTable"></document3>
        <img src="@/assets/media/interrogationRoom/phone.svg" class="phone" alt="">
    </div>

</template>

<script>
import document3 from "@/components/document3.vue";
export default {
  name: "phone-documents",
  components: {
    document3
  },
  data() {
    return {

  };
},
  methods: {
    backToTable() {
        this.$emit("backToTable", "cop");
    }
  },
};
</script>

<style scoped>
#phone-documents {
  background-image: url("@/assets/media/backGround.png");
  background-size: 100vw 100vh;
  height: 100vh;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  overflow: hidden;
}
.part1 {
  position: absolute;
  top: 50%;
  left: 40%;
  transform: translate(-50%, -50%);
  z-index: 2;
}
.phone {
    width: 15rem;
    position: relative;
    top: 10rem;
    right: 10rem;
}
</style>
