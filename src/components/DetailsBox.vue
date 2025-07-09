<template>
  <div id="details-box">
      <img
      v-show="note === 1"
        src="@/assets/media/part1documents/details1.png"
        alt="details"
        class="details1"
      />
      <img
      v-show="note === 2"
        src="@/assets/media/part1documents/details2.png"
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
