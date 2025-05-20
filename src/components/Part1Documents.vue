<template>
    <div id="part1-documents">
        <div v-if="page === 1" class="document1">
            <div class="marking1" id="cop" @click="choose" :class="{'chosen' : chosen === 'cop'}">
                
            </div>
            <div class="marking2" id="solider" @click="choose" :class="{'chosen' : chosen === 'solider'}">

            </div>
            <div class="que1">
                <input type="text" class="input" v-model="userInput11" @input="updateWrongCount" :class="userInput11 === '' ? '' : {'wrong' : !checkInput(userInput11)}"/>
                <select id="rank1" v-model="selectedRank" class="input" style="width: 2.9rem;">
                  <option v-for="rank in ranks" :key="rank" :value="rank" class="input">
                      {{ rank }}
                  </option>
                </select>
                <input type="text" class="input" v-model="userInput12" :class="userInput12 === '' ? '' : { 'wrong' : containsNumber(userInput12) }">
                <input type="text" class="input" v-model="userInput13" :class="userInput13 === '' ? '' : { 'wrong' : containsNumber(userInput13) }">
                <select id="forse1" v-model="selectedRank" class="input" style="width: 3.3rem;">
                  <option v-for="forse in forses" :key="forse" :value="forse" class="input bla">
                      {{ forse }}
                  </option>
                </select>
                <input type="text" class="input">
                <input type="text" class="input">
            </div>
         <div class="que2">
          <input type="text" class="input" id="p.n1" v-model="userInput21" @input="updateWrongCount" :class="userInput21 === '' ? '' : {'wrong' : !checkInput(userInput21)}"/>
                <select id="rank1" v-model="selectedRank" class="input" style="width: 2.9rem;">
                  <option v-for="rank in ranks" :key="rank" :value="rank" class="input">
                      {{ rank }}
                  </option>
                </select>
                <input type="text" class="input" v-model="userInput22" @input="updateWrongCount" :class="userInput22 === '' ? '' : { 'wrong' : containsNumber(userInput22) }">
                <input type="text" class="input" v-model="userInput23" @input="updateWrongCount" :class="userInput23 === '' ? '' : { 'wrong' : containsNumber(userInput23) }">
                <select id="forse1" v-model="selectedRank" class="input" style="width: 3.3rem;">
                  <option v-for="forse in forses" :key="forse" :value="forse" class="input bla">
                      {{ forse }}
                  </option>
                </select>
                <input type="text" class="input">
                <input type="text" class="input">
             </div>
             <div class="que3">
                 <input
                     type="text"
                     class="input3"
                />
             </div>
             <div class="que4">
              <select v-model="selectedHour" class="input4" id="time4">
                <option v-for="time in timeOptions" :key="time" :value="time">
                  {{ time }}
                </option>
              </select>
              <select v-model="selectedYear" class="input4">
                <option v-for="year in yearsArr" :key="year" :value="year">
                  {{ year }}
                </option>
              </select>
              <select v-model="selectedMonth" class="input4">
                <option v-for="month in monthsArr" :key="month" :value="month">
                  {{ month }}
                </option>
              </select>
              <select v-model="selectedDay" class="input4">
                <option v-for="day in daysArr" :key="day" :value="day">
                  {{ day }}
                </option>
              </select>
                 <!-- <input
                  v-for="field in secondFields"
                     :key="field"
                     type="text"
                     class="input4"
                   :id="`${field}4`"
                 /> -->
             </div>
             <div class="que4-text">
                 <input
                     type="text"
                    class="input"
                   id="text4"
                />
             </div>
             <div class="que5">
              <select v-model="selectedYear" class="input4 input5">
                <option v-for="year in yearsArr" :key="year" :value="year">
                  {{ year }}
                </option>
              </select>
              <select v-model="selectedMonth" class="input4 input5">
                <option v-for="month in monthsArr" :key="month" :value="month">
                  {{ month }}
                </option>
              </select>
              <select v-model="selectedDay" class="input4 input5">
                <option v-for="day in daysArr" :key="day" :value="day">
                  {{ day }}
                </option>
              </select>
              <select v-model="selectedHour" class="input4 input5" id="time5">
                <option v-for="time in timeOptions" :key="time" :value="time">
                  {{ time }}
                </option>
              </select>
              </div>
               <div class="que6">
                <select v-model="selectedYear" class="input4 input6">
                <option v-for="year in yearsArr" :key="year" :value="year">
                  {{ year }}
                </option>
              </select>
              <select v-model="selectedMonth" class="input4 input6">
                <option v-for="month in monthsArr" :key="month" :value="month">
                  {{ month }}
                </option>
              </select>
              <select v-model="selectedDay" class="input4 input6">
                <option v-for="day in daysArr" :key="day" :value="day">
                  {{ day }}
                </option>
              </select>
              <select v-model="selectedHour" class="input4 input6" id="time6">
                <option v-for="time in timeOptions" :key="time" :value="time">
                  {{ time }}
                </option>
              </select>
             </div>
             <button @click="checkAnswers" :disabled="wrongCount > 0">בדוק</button>
        
    </div>
    <button @click="page++">לעמוד הבא</button>
    <button @click="page--">לעמוד הקודם</button>
    <p class="detailBtn" @click="isOpen = !isOpen">פרטי העצור</p>
    <img v-show="isOpen" src="@/assets/media/part1documents/details.svg" alt="details" class="details">
    <div v-if="page === 2" class="document2">

    </div>
  </div>
 

</template>

<script>
export default {
  data() {
    return {
      wrongCount: 0,
      page: 1,
      secondFields: ['time', 'year', 'month', 'day'],
      ranks: ["טוראי", "רב'ט", "סמל","סמ'ר"],
      forses: ["האוויר","הההנדסה","הגנת גבולות", "החינוך והנוער", "משאבי האנוש","החימוש","הים","הלוגיסטיקה","המשטרה הצבאית","הקשר והתקשוב","הרבנות הצבאית", "הרגלים", "הרפואה", "השריון", "התותחנים", "המודיעין","הכללי"],
      REASON: "הטרדה מינית ומעשה מגונה בכוח",
      userInput11: '',
      userInput12: '',
      userInput13: '',
      userInput21: '',
      userInput22: '',
      userInput23: '',
      chosen: '',
      isOpen: false,
      selectedHour: '',
      timeOptions: [],
      yearsArr: [],
      monthsArr: ["ינואר", "פברואר","מרץ", "אפריל", "מאי", "יוני", "יולי", "אוגוסט", "ספטמבר", "אוקטובר", "נובמבר", "דצמבר"],
      daysArr: ["ראשון", "שני", "שלישי", "רביעי", "חמישי", "שישי", "שבת"]

    };
  },
  created() {
    this.generateTimeOptions();
    this.years();
  },
  methods: {
    generateTimeOptions() {
      const times = [];
      for (let h = 0; h < 24; h++) {
        for (let m = 0; m < 60; m+=5) {
          const hour = h.toString().padStart(2, '0');
          const minute = m.toString().padStart(2, '0');
          times.push(`${hour}:${minute}`);
        }
      }
      this.timeOptions = times;
    },
    years() {
      const year =[];
      for (let y = 1980; y < 2026; y++) {
        year.push(y.toString());
      }
      this.yearsArr = year;
  
    },
    checkAllFieldsFilled() {
    const inputs = document.querySelectorAll(".document1 input");
    const selects = document.querySelectorAll(".document1 select");

    for (let input of inputs) {
      if (input.value.trim() === "") {
        return false;
      }
    }

    for (let select of selects) {
      if (select.value.trim() === "") {
        return false;
      }
    }

    return true;
  },

  checkAnswers() {
    if (!this.checkAllFieldsFilled()) {
      alert("יש למלא את כל השדות לפני המשך.");
      return;
    }

    // כאן תמשיכי עם הלוגיקה שלך לבדיקה
    console.log("הכל מלא, אפשר להמשיך.");
  },
    choose(event) {
      if(event.target.id === 'cop') {
        this.chosen = 'cop';
      } else {
        this.chosen = 'solider';
      }
    },
    containsNumber(str) {
    return /\d/.test(str);
  },

    checkInput(value) {
  // בודק אם זה מספר ובדיוק 7 ספרות
  const isNumber = !isNaN(value);
  const isSevenDigits = /^\d{7}$/.test(value);

  return isNumber && isSevenDigits;

    },
  }
};
</script>

<style scoped>
.document1 {
  width: 40rem;
  height: 45rem;
  background-image: url('@/assets/media/part1documents/arrestReport.svg');
  background-size: 100% 100%;
  background-repeat: no-repeat;
}
.document2 {
  width: 40rem;
  height: 43rem;
  background-image: url('@/assets/media/part1documents/explainRights.svg');
  background-size: 100% 100%;
  background-repeat: no-repeat;
}
.details {
  position: absolute;
  bottom: 15rem;
  width: 16rem;
  right: 37rem;
}
.detailBtn {
  position: absolute;
  right: 41rem;
  bottom: 35rem;
  width: 5rem;
  text-align: center;
  color: white;
  font-size: 1rem;
  font-weight: bold;
  border-radius: 1rem;
  font-family: "rubik";
  padding: 1rem;
  background-color: #0E2C8E;
  cursor: pointer;
}
.detailBtn:hover {
  background-color: #0e277a;
}
.detailBtn:active {
  background-color: #123199;
}
.marking1 {
  position: relative;
  top: 8.6rem;
  right: 11.3rem;
  width: 2rem;
  height: 1rem;
  border: solid 2px rgb(0, 0, 0);
  border-radius: 100%;
  opacity: 0;
  cursor: pointer;

}
.marking2 {
  position: relative;
  top: 7.4rem;
  right: 15rem;
  width: 2rem;
  height: 1rem;
  border: solid 2px rgb(0, 0, 0);
  border-radius: 100%;
  opacity: 0;
  cursor: pointer;

}
.chosen {
  opacity: 1;
}
.que1 {
display: flex;
flex-direction: row;
align-items: center;
margin-top: -2.3rem;
}
.input {
    position: relative;
    margin-top: 11.5rem;
    right: 9.5rem;
    width: 2.7rem;
    border: solid 2px;
    border-radius: 5px;
    font-size: 0.7rem;

}
.que2 {
display: flex;
flex-direction: row;
align-items: center;
margin-top: -6.7rem;
}
.que3 {
display: flex;
flex-direction: row;
align-items: center;
}
.que4 {
display: flex;
flex-direction: row;
align-items: center;
}
.que4-text {
display: flex;
flex-direction: row;
align-items: center;
}
.input3 {
    width: 20rem;
    position: relative;
    margin-top: 2.5rem;
    right: 10rem;
    border: solid 2px;
    border-radius: 5px;
}
.input4 {
    position: relative;
    margin-top: 2rem;
    right: 19.4rem;
    width: 2rem;
    /* height: 1rem; */
    border: solid 2px;
    border-radius: 5px;
}
#time4 {
margin-left: 0.8rem;
width: 2.3rem;
}
#text4{
  position: relative;
  top: -11.3rem;
  right: 22rem;
  width: 3rem;
}
.input5 {
    position: relative;
    top: -10.2rem;
    right: 8rem;
    width: 2rem;
    border: solid 2px;
    border-radius: 5px;
}
.input6 {
    position: relative;
    top: -13.2rem;
    right: 18rem;
    width: 2rem;
    border: solid 2px;
    border-radius: 5px;
}
#time5 {
margin-right: 0.2rem;
width: 2.3rem;
}
#time6 {
margin-right: 0.2rem;
width: 2.3rem;
}
.correct {
  border: 2px solid green;
  background-color: #e0ffe0;
}

.wrong {
  border: 2px solid red;
  background-color: #ffe0e0;
}

 /* @media (max-width: 1470px) {
    .input4 {
      margin-top: 1.5rem;
    }
    #text4 {
      top: -11.4rem;
    }
}
@media (max-width: 1230px) {
    .input4 {
      margin-top: 1.1rem;
    }
    #text4 {
      top: -11.4rem;
    }
} */

</style>
