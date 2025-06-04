<template>
    <div id="cop-documents">
        <document4 class="part1"></document4>
    </div>

</template>

<script>
import document4 from "@/components/document4.vue";
export default {
  name: "cop-documents",
  components: {
    document4
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
#cop-documents {
  width: 100%;
  height: 100%;
  background-color: #7B736E;
  overflow: hidden;
}
 .part1 {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 2;
}
</style>
