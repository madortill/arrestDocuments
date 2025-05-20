<template>
<svg width="1394" height="1003" viewBox="0 0 1394 1003" fill="none" xmlns="http://www.w3.org/2000/svg">
<rect y="259.546" width="1262.1" height="767.983" transform="rotate(-11.8674 0 259.546)" fill="#846363" class="bla"/>
<rect x="346.677" y="695" width="145.203" height="199.266" transform="rotate(6.24503 346.677 695)" fill="#E8E8E8"/>
<rect x="358.677" y="683" width="145.203" height="199.266" transform="rotate(6.24503 358.677 683)" fill="white"/>
<line x1="373.284" y1="732.512" x2="478.785" y2="742.787" stroke="black" stroke-width="5"/>
<line x1="369.904" y1="767.217" x2="475.405" y2="777.493" stroke="black" stroke-width="5"/>
<line x1="362.242" y1="845.882" x2="467.743" y2="856.158" stroke="black" stroke-width="5"/>
<line x1="366.298" y1="804.236" x2="471.799" y2="814.511" stroke="black" stroke-width="5"/>
<rect x="173" y="347.574" width="90.3566" height="157.44" transform="rotate(-15.1237 173 347.574)" fill="black"/>
<rect x="182" y="351.515" width="74.7973" height="145.071" transform="rotate(-15.1237 182 351.515)" fill="#D9D9D9"/>
<rect x="358.335" y="683" width="145.718" height="199.285" transform="rotate(5.75106 358.335 683)" fill="white" fill-opacity="0.08"  @click="zoomDocuments" :class="{'mouse' : time === 0}" />
</svg>


</template>

<script>
export default {
  name: "table",
  data() {
     return {
      time: 0,
     };
  },
  methods: {
    zoomDocuments () {
        this.$emit("zoom");
    }
  }
}

</script>

<style scoped>
  .mouse {
    cursor: pointer;
  }
</style>