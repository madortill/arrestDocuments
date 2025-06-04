<template>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    xmlns:xlink="http://www.w3.org/1999/xlink"
    viewBox="0 0 1920 1080"
    class="full-svg"
  >
    <defs>
      <radialGradient
        id="radial-gradient"
        cx="977"
        cy="542.91"
        fx="1098.73"
        fy="-107.12"
        r="854.89"
        gradientUnits="userSpaceOnUse"
      >
        <stop offset="0" stop-color="#4b495a" />
        <stop offset="1" stop-color="#231f20" />
      </radialGradient>
      <linearGradient
        id="linear-gradient"
        x1="960"
        y1="0"
        x2="960"
        y2="1080"
        gradientUnits="userSpaceOnUse"
      >
        <stop offset="0" stop-color="#fff" />
        <stop offset="1" stop-color="#231f20" />
      </linearGradient>
    </defs>

    <g class="cls-4">
      <g id="_חלקים" data-name="חלקים">
        <image
          :xlink:href="tableImg"
          width="3840"
          height="2160"
          transform="translate(-193.86 -251.85) scale(.61)"
        />
        <image
        :href="papersImg"
          width="3840"
          height="2160"
          transform="translate(-56.52 -191.98) scale(.61)"
          @click="bla"
          :style="{ pointerEvents: 'auto', cursor: 'pointer' }"
        />
        <image
          :xlink:href="ecreepImg"
          width="3840"
          height="2160"
          transform="translate(-193.86 -251.85) scale(.61)"
          class="papa"
        />
        <image
          :xlink:href="policemanImg"
          width="3840"
          height="2160"
          transform="translate(-193.86 -251.85) scale(.61)"
          @click="moveToCop"
          :class="{ glow: time === 1 }"
           :style="{ pointerEvents: 'auto', cursor: 'pointer' }"
        />
        <image
          :xlink:href="phoneImg"
          width="3840"
          height="2160"
          transform="translate(-193.86 -251.85) scale(.61)"
          class="mouse"
          :class="{ glow: time === 1, mouse: time === 1, disabled: time != 1 }"
          :disabled="time != 1"
          @click="moveToPhone"
        />
      </g>
    </g>
  </svg>
</template>

<script>
import tableImg from "@/assets/media/interrogationRoom/table.png";
import papersImg from "@/assets/media/interrogationRoom/papers.png";
import ecreepImg from "@/assets/media/interrogationRoom/ecreep.png";
import policemanImg from "@/assets/media/interrogationRoom/policeman.png";
import phoneImg from "@/assets/media/interrogationRoom/phone-on-table.png";

export default {
  name: "table",
  data() {
    return {
      tableImg,
      papersImg,
      ecreepImg,
      policemanImg,
      phoneImg,
      time: 0,
    };
  },
  methods: {
    zoomDocuments() {
      console.log("hi");
      this.$emit("zoom");
      this.time = 1;
      console.log("hi");
    },
    moveToPhone() {
      console.log("hiii");
      this.$emit("move");
      this.time = 2;
    },
    bla() {
      console.log("hii");
    },
    moveToCop() {
      this.$emit("move");
    }
  },
};
</script>

<style scoped>
.full-svg {
  width: 100%;
  height: 90vh;
  display: block;
  margin-top: 3rem;
}
.mouse {
  cursor: pointer;
}
.glow {
  filter: drop-shadow(0 0 20px #00e5ff);
  transition: all 0.3s ease;
}
.disabled {
  pointer-events: none;
}

.cls-1 {
  opacity: 0.75;
}

.cls-2 {
  fill: url(#linear-gradient);
  mix-blend-mode: darken;
  opacity: 0.35;
}

.cls-3 {
  fill: url(#radial-gradient);
}

.cls-4 {
  isolation: isolate;
}

.cls-5 {
  mix-blend-mode: color-dodge;
  opacity: 0.72;
}

.cls-6 {
  opacity: 0.69;
}
.papa {
  pointer-events: none;
}
</style>
