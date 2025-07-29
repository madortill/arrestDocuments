<template>
  <div id="information">
    <div v-if="docNum === 1" class="container">
      <p class="text text1">
        בדף זה נתעד את פרטי העצור, פרטי העוצר, סיבת המעצר, שעת המעצר המדוייקת,
        תאריך וחתימה
      </p>
    </div>
    <div v-if="docNum === 2" class="container">
      <p class="text">הסברת זכויות לעצור:</p>
      <ul>
        <li class="text text2">הודעה לאדם קרוב על דבר מעצרו.</li>
        <li class="text text2">היוועצות בעורך דין.</li>
        <li class="text text2">זכות השתיקה- הזכות לאי הפללה עצמית.</li>
        <li class="text text2">הזכות לאי פרסום שמו של הנחקר בכלי התקשורת.</li>
      </ul>
    </div>
    <div v-if="docNum === 3" class="container">
      <p class="text text3">
        נתקשר לגורמים הרלוונטים על מנת לעדכן אותם בדבר מעצר החשוד, כמו כן נתעד
        את השיחה על גבי הטופס וגם ביומן החקירות:
      </p>
      <ul>
        <li class="text text3">יחידת החייל</li>
        <li class="text text3">קצין פניות הציבור</li>
        <li class="text text3">קמב"ץ מצ"ח- רק במקרים של אלימות חמורה או מין</li>
        <li class="text text3">חמ"ל ליווים</li>
      </ul>
    </div>
    <div v-if="docNum === 4" class="container">
      <p class="text text4">
        השימוע היא האפשרות הניתנת לחייל העצור לטעון את טענותיו בפני הגורם פוקד
        המעצר, בדבר החזקתו בתנאי מעצר.
      </p>
      <p class="text text4">
        על גבי השימוע נכתוב דברים רלוונטים שהעצור צריך על מנת להיות במעצר, כגון
        כדורים, תרופות, בגדים וכו.
      </p>
    </div>
    <div v-if="docNum === 5" class="container">
      <p class="text text5">
        טופס המתעד את מימוש זכויות החשוד עליו יחתום החשוד. אנחנו ניתן לחשוד את
        האפשרות לממש אותן.
      </p>
      <p class="text text5-up">
        במידה והעצור בחר שלא לממש זכותו באופן מידי עם הודעה על מעצרו, הוא ראשי
        לממשן גם במועד מאוחר יותר. במקרה כזה, נתעד את מימוש הזכויות ע"ג טופס
        מימוש מאוחר של הזכויות.
      </p>
    </div>
    <div v-if="docNum === 6" class="container">
      <p class="text text6">
        לנחקר האפשרות לבקש מבית הדין למנוע את פרסום שמו או פרטיו האישיים מטענות
        שלפגיעה בפרטיות. את הבקשה אין חובה למלא במידה והחשוד איננו מעוניין.
        במידה ובוחר למלא נשים לב כי כלל הפרטים של החשוד היו כתובים על גבי הדף.
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "information",
  props: ["docNum"],
  components: {},
  data() {
    return {
      doc: 1,
    };
  },
  methods: {},
};
</script>

<style scoped>
.container {
  position: absolute;
  top: 6.5rem;
  right: -11.5rem;
  height: 15rem;
  width: 11rem;
  background-image: url("@/assets/media/information.png");
  background-size: 100% 100%;
  background-repeat: no-repeat;
  padding: 2rem;
}
.text {
  font-family: "dana";
  color: rgb(0, 0, 0);
  direction: rtl;
  font-size: 1.2rem;
  font-weight: 700;
  position: relative;
  /* top: -1rem; */
  right: -0.5rem;
}
.text1 {
  width: 12rem;
  text-align: center;
}
.text2 {
  font-size: 1.1rem;
  width: 12rem;
  position: relative;
  top: -0.5rem;
  right: -2rem;
}
.text3 {
  font-size: 1.1rem;
  width: 12rem;
  position: relative;
  top: -1.4rem;
  right: -1rem;
}
.text4 {
  width: 12rem;
  text-align: center;
  position: relative;
  top: -1.2rem;
  right: -0.5rem;
}
.text5 {
  width: 12rem;
  text-align: center;
  font-size: 1.1rem;
  position: relative;
  top: -1.3rem;
}
.text5-up {
  width: 12rem;
  text-align: center;
  font-size: 1.1rem;
  position: relative;
  top: -1.7rem;
}
.text6 {
  width: 12rem;
  text-align: center;
  font-size: 1.2rem;
  position: relative;
  top: -1.2rem;
}
</style>
