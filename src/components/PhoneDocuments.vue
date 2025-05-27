<template>
    <div id="phone-documents">
        <document3 class="part1"></document3>
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
    
  },
};
</script>

<style scoped>
.part1 {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 2;
}
</style>
