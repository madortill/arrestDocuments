<template>
  <div id="phone-documents">
    <document3 class="part1" @backToTable="backToTable"></document3>
    <!-- <img
      src="@/assets/media/interrogationRoom/phone.svg"
      class="phone"
      alt=""
    /> -->
  </div>
</template>

<script>
import document3 from "@/components/document3.vue";
export default {
  name: "phone-documents",
  components: {
    document3,
  },
  data() {
    return {};
  },
  methods: {
    backToTable() {
      this.$emit("backToTable", "cop");
    },
  },
};
</script>

<style scoped>
#phone-documents {
  background-image: url("@/assets/media/backGround.png");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  min-height: 100vh; /* במקום height */
  overflow-y: auto; /* גלילה אנכית */
  position: relative; /* כדי לאפשר מיקום יחסי של תוכן */
}
.part1 {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-58%, -50%);
  margin-right: 5rem;
  z-index: 2;
}

@media (max-width: 1170px) {
  .phone {
    top: 14rem;
    right: 6.5rem;
  }
}
@media (max-width: 930px) {
.part1 {
  transform: translate(-50%, -50%);
}
}
</style>
