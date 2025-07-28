<template>
  <div id="details-box">
      <img
      v-show="note === 1"
        src="@/assets/media/details/details1.png"
        alt="details"
        class="details1"
      />
      <img
      v-show="note === 2"
        src="@/assets/media/details/details2.png"
        alt="details"
        class="details2"
      />
      <img
      v-show="note === 3"
        src="@/assets/media/details/details3.png"
        alt="details"
        class="details2"
      />
      <img
      v-show="note === 4"
        src="@/assets/media/details/details4.png"
        alt="details"
        class="details2"
      />
      <img
      v-show="note === 5"
        src="@/assets/media/details/details5.png"
        alt="details"
        class="details2"
      />
      <img
      v-show="note === 6"
        src="@/assets/media/details/details6.png"
        alt="details"
        class="details2"
      />
  </div>
</template>

<script>
export default {
  name: "details-box",
  props: ["note"],
  components: {},
  data() {
    return {};
  },
  methods: {},
};
</script>

<style scoped>
.details1 {
  width: 18rem;
  position: absolute;
}
.details2 {
  width: 14.5rem;
  position: absolute;
}
</style>
