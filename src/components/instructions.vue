<template>
  <div id="instructions">
    <div class="inst">
    <img src="@/assets/media/interrogationRoom/close.svg" class="closeBtn" @click="closeInstruction" alt="close">
    <p class="instText">הגעתם לחדר החקירות!</p>
    <p class="instText">בעזרת המידע שיש ברשותכם אתם תידרשו למלא את מסמכי המעצר השונים.</p>
    <p class="instText">שימו לב! לא תוכלו לעבור הלאה עד שאתם לא תמלאו את כל השדות במסמך(כולל תיבות סימון, חתימה והקפה בעיגול בעת הצורך).</p>
    <p class="instText">במקרה שחלק מתשובותיכם יהיו שגויות הן יסומנו באדום, תצטרכו לתקן אותן ורק אז תוכלו לעבור הלאה.</p>
    <p class="instText">מאמינים בכם ובטוחים שתמלאו את המסמכים כראוי וכך תעצרו את החשוד במהירות האפשרית!</p>
</div>
<p v-if="isIphone" class="iphone">שימו לב שהמרכאות לאורך הלומדה הן כאלה(") ולא באלכסון(”).</p>
  </div>
</template>

<script>
export default {
  name: "instructions",
  components: {},
  data() {
    return {
      isIphone: false,
    };
  },
  mounted() {
  const isIOS = /iPad|iPhone|iPod/.test(navigator.userAgent) 
             || (navigator.platform === 'MacIntel' && navigator.maxTouchPoints > 1);
  this.isIphone = isIOS;
},
  methods: {
    closeInstruction() {
      this.$emit("close");
    },
  }
};
</script>

<style scoped>
#instructions {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 8; /* שיהיה מעל הכול */
  overflow: hidden;
}
.inst {
    background-color: #EAEAEA;
    border: solid #0e2c8e 0.3rem;
    border-radius: 1.5rem;
    font-family: "rubik";
    text-align: center;
    padding: 1.7rem;
    z-index: 1;
}
.instText {
    font-family: "rubik";
    width: 15rem;
    font-size: 1.1rem;
    
}
.closeBtn {
    width: 2.5rem;
    margin-left: 13rem;
    /* pointer-events: auto; */
    cursor: pointer;
}
.iphone {
  position: absolute;
  top: 1rem;
  right: 7rem;
  z-index: 2;
  color: #ff0000;
  width: 12rem;
  font-family: "rubik";
  font-size: 0.9rem;
  text-align: center;
  /* font-weight: bold; */
}
</style>
