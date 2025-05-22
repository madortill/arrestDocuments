<template>
    <div id="basic-documents">
        <document1 class="part1"></document1>
    </div>

</template>

<script>
import document1 from '@/components/document1.vue';

export default {
  name: "basic-documents",
  components: {
    document1
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
