<template>
  <div>
    <b-container>
      <b-row>
        <b-col xs="4" offset-xs="4">
          <label for="dateofbirth-datepicker"><h2>Дата рождения:</h2></label>
          <b-form-datepicker
            id="dateofbirth-datepicker"
            v-model="date"
            class="mb-2"
            size="lg"
            :locale="locale"
            offset="60"
            placeholder="Выберете дату"
            v-bind="labels[locale] || {}"
            year-button
            start-weekday="1"
            initial-date="2000-01-01"
          >
          </b-form-datepicker>
        </b-col>
      </b-row>
      <b-row v-if="preFinalA!=null">
        <b-col xs="4" offset-xs="4"><h3>Хроника Жизни</h3></b-col>
      </b-row>
      <hr/>
      <b-row v-if="preFinalA!=null">
        <b-col xs="1" offset-xs="3">Р</b-col>
        <b-col xs="1">П</b-col>
        <b-col xs="6">Периоды</b-col>
      </b-row>
      <b-row v-if="preFinalA!=null">
        <template v-for="(item,index) in preFinalA">
          <b-col v-if="index==0" xs="1" offset-xs="3" :key="index">{{item}}</b-col>
          <b-col v-if="index==1" xs="1" :key="index">{{item}}</b-col>
          <b-col v-if="index==2" xs="6" :key="index">{{item}}</b-col>
        </template>
      </b-row>
      <b-row v-if="sum!=null">
        <b-col xs="1" offset-xs="3">{{sum}}</b-col>
        <b-col xs="1"></b-col>
        <b-col xs="6"></b-col>
      </b-row>
      <b-row v-if="FinalA!=null">
        <template v-for="(item,index) in FinalA">
          <b-col v-if="index==0" xs="1" offset-xs="3" :key="index">{{item}}</b-col>
          <b-col v-if="index==1" xs="1" :key="index">{{item}}</b-col>
          <b-col v-if="index==2" xs="6" :key="index">{{item}}</b-col>
        </template>
      </b-row>
      <hr/>
      <b-row v-if="table3aResult!=null">
        <b-col xs="12"><h3>Потенциал личности</h3></b-col>
      </b-row>
      <b-row v-if="table3aResult!=null">
        <b-col xs="12"><h5>(показатели чакр в % от 0 до 100)</h5></b-col>
      </b-row>
      <hr/>
      <b-row v-if="table3aResult!=null">
        <b-col xs="4"><h5>Физический</h5>1 – 2 чакра</b-col>
        <b-col xs="4"><h5>Эмоциональный</h5>3 – 4 чакра</b-col>
        <b-col xs="4"><h5>Интеллектуальный</h5>5 – 6 чакра</b-col>
      </b-row>
      <b-row v-if="table3aResult!=null">
        <template v-for="(item,index) in table3aResult">
          <b-col v-if="index==0" xs="4" :key="index">{{item}}</b-col>
        </template>
        <template v-for="(item,index) in table3bResult">
          <b-col v-if="index==0" xs="4" :key="index">{{item}}</b-col>
        </template>
        <template v-for="(item,index) in table3cResult">
          <b-col v-if="index==0" xs="4" :key="index">{{item}}</b-col>
        </template>
      </b-row>
      <b-row v-if="table3aResult!=null">
        <template v-for="(item,index) in table3aResult">
          <b-col v-if="index==1" xs="4" :key="index">{{item}}</b-col>
        </template>
        <template v-for="(item,index) in table3bResult">
          <b-col v-if="index==1" xs="4" :key="index">{{item}}</b-col>
        </template>
        <template v-for="(item,index) in table3cResult">
          <b-col v-if="index==1" xs="4" :key="index">{{item}}</b-col>
        </template>
      </b-row>
      <hr/>
      <b-row v-if="yang!=null">
        <b-col xs="6"><h5>Инь (Женское)</h5></b-col>
        <b-col xs="6"><h5>Ян (Мужское)</h5></b-col>
      </b-row>
      <b-row v-if="yang!=null">
        <b-col xs="6">{{yin}}</b-col>
        <b-col xs="6">{{yang}}</b-col>
      </b-row>
      <hr/>
      <b-row v-if="sex!=null">
        <b-col xs="4"><h5>Хочу</h5></b-col>
        <b-col xs="4"><h5>Могу</h5></b-col>
        <b-col xs="4"><h5>Секс потенциал</h5></b-col>
      </b-row>
      <b-row v-if="sex!=null">
        <b-col xs="4">{{want}}</b-col>
        <b-col xs="4">{{can}}</b-col>
        <b-col xs="4">{{sex}}</b-col>
      </b-row>
      <hr/>
      <b-row v-if="table4Result!=null">
        <b-col xs="12"><h3>Эмоциональный тип</h3></b-col>
      </b-row>
      <b-row v-if="table4Result!=null">
        <template v-for="(item,index) in table4Result">
          <b-col v-if="index==0" xs="12" :key="index"><h5>{{item}}</h5></b-col>
        </template>
      </b-row>
      <hr/>
      <b-row v-if="table4Result!=null">
        <b-col xs="6"><h5>«Я»</h5></b-col>
        <b-col xs="6"><h5>«Мы»</h5></b-col>
      </b-row>
      <b-row v-if="table4Result!=null">
        <template v-for="(item,index) in table4Result">
          <b-col v-if="index>0" xs="6" :key="index"><h5>{{item}}</h5></b-col>
        </template>
      </b-row>
      <hr/>
      <b-row v-if="leapYear">
        <b-col xs="12"><h5>Високосный год</h5></b-col>
      </b-row>
      <hr/>
    </b-container>
  </div>
</template>

<script>
import table1 from "../data/table1.json";
import table2 from "../data/table2.json";
import table3a from "../data/table3a.json";
import table3b from "../data/table3b.json";
import table3c from "../data/table3c.json";
import table4 from "../data/table4.json";
export default {
  name: "Main",
  data() {
    return {
      date: null,
      dob: null,
      leapYear: null,
      year: null,
      month: null,
      day: null,
      yang: null,
      yin: null,
      intuition: null,
      logic: null,
      want: null,
      can: null,
      sex: null,
      sum: null,
      preFinalA: null,
      FinalA: null,
      table3aResult: null,
      table3bResult: null,
      table3cResult: null,
      table4Result: null,
      locale: "ru-Ru",
      labels: {
        "ru-Ru": {
          labelPrevYear: 'Предыдущий Год',
          labelPrevMonth: 'Предыдущий Месяц',
          labelCurrentMonth: 'Текущий Месяц',
          labelNextMonth: 'Следующий Месяц',
          labelNextYear: 'Следующий Год',
          labelToday: 'Сегодня',
          labelSelected: 'Выбраная Дата',
          labelNoDateSelected: 'Дата не выбрана',
          labelCalendar: 'Календарь',
          labelNav: 'Навигация для Календаря',
          labelHelp: 'Используйте стрелки клавиатуры чтобы изменить день'
        }
      }
    };
  },
  watch: {
    date: function(val) {
      this.dob = this.$moment(val);
      this.leapYear = this.dob.isLeapYear();
      this.year = this.dob.year();
      this.month = this.dob.month() + 1;
      this.day = this.dob.date();

      //get table data
      //calc month for leap year cases
      let tableM =
        this.month === 2 && this.leapYear === true
          ? this.month + "l"
          : this.month;

      let yearA = table1[this.year];
      let monthA = table2[tableM];
      let dInM = this.$moment(this.dob).daysInMonth();
      let dayAn = dInM - this.day;
      let dayA = [dayAn, dayAn, dayAn];

      let sumA = [0, 0, 0];
      let limit = [23, 28, 33];

      for (let i = 0; i < sumA.length; i++) {
        sumA[i] = yearA[i] + monthA[i] + dayA[i];
        while (sumA[i] > limit[i]) {
          sumA[i] = sumA[i] - limit[i];
        }
      }

      let table3aResult = table3a[sumA[0]];
      let table3bResult = table3b[sumA[1]];
      let table3cResult = table3c[sumA[2]];

      let table4Result = table4[sumA[1]];

      //get yin/yang
      let t3aN = table3aResult[0].split("-");
      let t3bN = table3bResult[0].split("-");
      let t3cN = table3cResult[0].split("-");

      let yang = parseInt(t3aN[1]) + parseInt(t3bN[0]) + parseInt(t3bN[1]);
      let yin = parseInt(t3aN[0]) + parseInt(t3cN[0]) + parseInt(t3cN[1]);

      this.yang = yang;
      this.yin = yin;

      //get intuition/logic

      let intuition = parseInt(t3bN[0]) + parseInt(t3cN[0]);
      let logic = parseInt(t3bN[1]) + parseInt(t3cN[1]);
      
      this.intuition = intuition;
      this.logic = logic;

      //get want/can

      let want = yang > yin ? yang - yin : yin - yang;
      let can = parseInt(t3aN[0]);
      let sex = want*can;

      this.want = want;
      this.can = can;
      this.sex = sex;

      //get code
      //get each number
      let n1 = parseInt(this.year / 1000);
      let n2 = parseInt((this.year / 100) % 10);
      let n3 = parseInt((this.year / 10) % 10);
      let n4 = parseInt(this.year % 10);
      let n5 = parseInt(this.month / 10);
      let n6 = parseInt(this.month % 10);
      let n7 = parseInt(this.day / 10);
      let n8 = parseInt(this.day % 10);

      let nArray = [n1, n2, n3, n4, n5, n6, n7, n8];

      //get sum of all date numbers
      let sum = 0;
      nArray.forEach(element => {
        sum += element;
      });
     
      while (sum >= 10) {
        sum = sum >= 10 ? parseInt(sum / 10) + parseInt(sum % 10) : sum;
      }
      this.sum = sum;

      let firstN = parseInt(this.year) * parseInt("" + n7 + n8 + n5 + n6);
      let nArrayMD = [n5, n6, n7, n8];
      let sumMD = 0;
      nArrayMD.forEach(element => {
        sumMD += element;
      });
      sumMD = sumMD >= 10 ? parseInt(sumMD / 10) + parseInt(sumMD % 10) : sumMD;
      let preFinalA = [
        sumMD,
        parseInt(firstN.toString().charAt(0)),
        firstN.toString().substr(1)
      ];

      this.preFinalA = preFinalA;

      let fA = [
        parseInt(preFinalA[2] / 100000),
        parseInt((preFinalA[2] / 10000) % 10),
        parseInt((preFinalA[2] / 1000) % 10),
        parseInt((preFinalA[2] / 100) % 10),
        parseInt((preFinalA[2] / 10) % 10),
        parseInt(preFinalA[2] % 10)
      ];

      for (let i = 0; i < fA.length; i++) {
        fA[i] = fA[i] + sum >= 10 ? parseInt((fA[i] + sum) / 10) + parseInt((fA[i] + sum) % 10) : (fA[i] + sum);
      }

      let fAfinal = "";
      fA.forEach(element => {
        fAfinal += element;
      });

      let FinalA = [
        preFinalA[0] + sum >= 10 ? parseInt((preFinalA[0] + sum) / 10) + parseInt((preFinalA[0] + sum) % 10) : preFinalA[0] + sum,
        preFinalA[1] + sum >= 10 ? parseInt((preFinalA[1] + sum) / 10) + parseInt((preFinalA[1] + sum) % 10) : preFinalA[1] + sum,
        parseInt(fAfinal)
      ];

      this.FinalA = FinalA;

      this.table3aResult = table3aResult;
      this.table3bResult = table3bResult;
      this.table3cResult = table3cResult;
      this.table4Result = table4Result;

    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  div{
    word-wrap: break-word;
    word-break: break-all;
  }
  .container{
    margin-bottom: 50px;
  }
</style>
