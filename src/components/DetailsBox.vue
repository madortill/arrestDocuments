<template>
  <div id="details-box">
      <img
        src="@/assets/media/part1documents/details1.svg"
        alt="details"
        class="details"
      />
  </div>
</template>

<script>
export default {
  name: "details-box",
  components: {},
  data() {
    return {};
  },
  methods: {},
};
</script>

<style scoped>
.details {
  width: 18rem;
  position: absolute;
}
.red {
  background-color: red;
  padding: 3rem;
  font-size: 3rem;
}
</style>
