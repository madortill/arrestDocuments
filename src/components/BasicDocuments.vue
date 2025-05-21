<template>
    <div id="basic-documents">
        <part-1-documents class="part1"></part-1-documents>
    </div>

</template>

<script>
import Part1Documents from '@/components/Part1Documents.vue';

export default {
  name: "basic-documents",
  components: {
    Part1Documents
  },
  data() {
     
  },
  methods: {
    
  }
}
</script>

<style scoped>
#basic-documents {
    width: 100%;
    height: 100%;
    background-color: #846363;
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
