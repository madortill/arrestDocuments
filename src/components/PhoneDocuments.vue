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
        this.$emit("backToTable", "suspect");
    }
  },
};
</script>

<style scoped>
#phone-document {
  width: 100%;
  height: 100%;
  background-color: #846363;
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
    width: 20rem;
    position: relative;
    top: 10rem;
    right: 10rem;
}
</style>
