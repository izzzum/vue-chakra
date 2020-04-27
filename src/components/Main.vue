<template>
  <div>
    <b-container>
      <b-row>
        <b-col xs="4" offset-xs="4">
          <label for="dateofbirth"><h2 class="group-title">Дата рождения</h2></label>
          <br />
          <font-awesome-icon :icon="calendar" size="2x" class="calendar-icon titleColor" />
          <date-pick 
            v-model="date"
            class="mb-2 calendar"
            :selectableYearRange="{from: 1900, to: 2151}"
            :nextMonthCaption="nextMonthCaption"
            :prevMonthCaption="prevMonthCaption"
            :weekdays="weekdays"
            :months="months"
            :inputAttributes="{
              class: 'form-control', 
              id: 'dateofbirth', 
              placeholder: 'Выберите дату', 
              autocomplete:'off'}"
          >
          </date-pick>
        </b-col>
      </b-row>
      
      <b-row v-if="preFinalA!=null">
        <b-col xs="4" offset-xs="4"><h3 class="group-title">Код судьбы</h3></b-col>
      </b-row>
      
      <b-row v-if="preFinalA!=null">
        <b-col xs="12" offset-xs="3"><span class="underline fate-code-title"><b>Р</b><b>К</b><b>ПЕРИОДЫ</b></span></b-col>
      </b-row>
      <b-row v-if="preFinalA!=null">
        <b-col xs="12" offset-xs="3" class="font-size-numbers">
          <template v-for="(item,index) in preFinalA">
            <span :class="{ 'red': index==0, 'purple': index==1, 'spaced-text': index==2, 'add-space': item.length==5&item>10}" :key="(Math.random()*10)+index">{{item}}</span><template v-if="index!=2">/ </template>
          </template>
        </b-col>
      </b-row>
      <b-row v-if="FinalA!=null" class="move-up">
        <b-col xs="12" offset-xs="3" class="font-size-numbers">
          <span class="underline">
            <template v-for="(item,index) in FinalA">
              <span :class="{ 'red': index==0, 'purple': index==1, 'spaced-text': index==2, 'add-space': item.length==5&item>10}" :key="(Math.random()*10)+index">{{item}}</span><template v-if="index!=2">/ </template>
            </template>
          </span>
        </b-col>
      </b-row>
      <b-row v-if="sum!=null">
        <b-col xs="12" offset-xs="3" class="smaller-font bold">{{sum}} ВОПЛОЩЕНИЕ</b-col>
      </b-row>
      
      <b-row v-if="graph!=null">
        <b-col xs="12"><h3 class="group-title space-top">Потенциал чакр</h3></b-col>
      </b-row>
      <b-row v-if="graph!=null">
        <b-col xs="12" class="yoga-bg">
          <p v-for="(item) in graph" :class="item.color" :key="(Math.random()*10)+item.value"><span>{{item.name}} {{item.value}}%</span></p>
        </b-col>
      </b-row>
      
      <b-row v-if="phys!=null">
        <b-col xs="12"><h3 class="group-title space-top">Контуры</h3></b-col>
      </b-row>
      <b-row v-if="phys!=null">
        <div class="centered-box">
          <b-col v-if="phys!=null" class="text-center text-title" xs="12"><span class="outlines-title">ФИЗИЧЕСКИЙ</span> <span class="outlines red">{{phys}}</span></b-col>
        </div>
      </b-row>
      <b-row v-if="emotion!=null">
        <div class="centered-box">
          <b-col v-if="emotion!=null" class="text-center text-title" xs="12"><span class="outlines-title">ЭМОЦИОНАЛЬНЫЙ</span> <span class="outlines green">{{emotion}}</span></b-col>
        </div>
      </b-row>
      <b-row v-if="intel!=null">
        <div class="centered-box">
          <b-col v-if="intel!=null" class="text-center text-title" xs="12"><span class="outlines-title">ИНТЕЛЛЕКТУАЛЬНЫЙ</span> <span class="outlines purple">{{intel}}</span></b-col>
        </div>
      </b-row>
      
      <b-row v-if="phys!=null">
        <b-col xs="12"><h3 class="group-title space-top">Дополнительно</h3></b-col>
      </b-row>

      <div class="centered-box">
        <b-row v-if="table4Result!=null">
          <b-col xs="6">
              <span class="addon-title float-left"><span class="name">"Я"</span> <span class="m-left we" v-if="iam!=null">"МЫ"</span></span>
          </b-col>
          <b-col xs="6">
              <span class="addon-title float-right"><span class="name m-right yang">Ян</span> <span class="move-right" v-if="yang!=null">Инь</span></span>
          </b-col>
        </b-row>

        <b-row class="space-bot" v-if="table4Result!=null">
          <b-col xs="6">
              <span class="addon-title float-left"><span class="name black-value blue">{{iam}}</span> <span :class="{ 'more': iam.length==2}" class="black-value m-left green we-val" v-if="we!=null">{{we}}</span></span>
          </b-col>
          <b-col xs="6">
              <span class="addon-title float-right"><span class="name m-right yang black-value brown">{{yang}}</span> <span class="black-value orange move-right" v-if="yin!=null">{{yin}}</span></span>
          </b-col>
        </b-row>

        <b-row v-if="want!=null">
          <b-col xs="6">
              <span class="addon-title float-left"><span class="name want">Хочу:</span> <span class="black-value orange">{{want}}</span></span>
          </b-col>
          <b-col xs="6">
              <span class="addon-title float-right"><span class="name">Интуиция:</span> <span class="black-value blue move-right">{{intuition}}</span></span>
          </b-col>
        </b-row>

        <b-row class="space-bot" v-if="can!=null">
          <b-col xs="6">
              <span class="addon-title float-left"><span class="name">Могу:</span> <span class="black-value red">{{can}}</span></span>
          </b-col>
          <b-col xs="6">
              <span class="addon-title float-right"><span class="name">Логика:</span> <span class="black-value purple move-right">{{logic}}</span></span>
          </b-col>
        </b-row>
        
        <b-row v-if="sex!=null">
          <b-col xs="12">
            <span class="addon-title xl-longer">Секс потенциал</span>
          </b-col>
        </b-row>
        <b-row class="space-bot" v-if="sex!=null">
          <b-col xs="12">
            <span class="addon-title xl-longer"><span class="black-value orange">{{sex}}</span></span>
          </b-col>
        </b-row>
        
        
        <b-row v-if="table4Result!=null">
          <b-col xs="12">
              <span class="addon-title xl-longer">Эмоциональный тип</span>
          </b-col>
        </b-row>
        <b-row v-if="table4Result!=null">
          <template v-for="(item,index) in table4Result">
            <b-col v-if="index==0" xs="12" :key="(Math.random()*10)+index" class="green"><h5 class="year text-center">{{item}}</h5></b-col>
          </template>
        </b-row>
      </div>

      <b-row v-if="leapYear">
        <b-col xs="12"><h5 class="bg-bot space-top year">Високосный год</h5></b-col>
      </b-row>
      <b-row v-else-if="leapYear==false">
        <b-col xs="12"><h5 class="bg-bot space-top year">Не Високосный год</h5></b-col>
      </b-row>
      
    </b-container>
  </div>
</template>

<script>
import DatePick from 'vue-date-pick';
import 'vue-date-pick/dist/vueDatePick.css';
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import { faCalendarAlt } from "@fortawesome/free-solid-svg-icons";

import table1 from "../data/table1.json";
import table2 from "../data/table2.json";
import table3a from "../data/table3a.json";
import table3b from "../data/table3b.json";
import table3c from "../data/table3c.json";
import table4 from "../data/table4.json";
export default {
  name: "Main",
  components: {
    DatePick,
    FontAwesomeIcon,
  },
  data() {
    return {
      space: '&nbsp;',
      calendar: faCalendarAlt,
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
      phys: null,
      intel: null,
      emotion: null,
      table4Result: null,
      we: null,
      iam: null,
      nextMonthCaption: 'Следующий Месяц',
      prevMonthCaption: 'Предыдущий Месяц',
      setTimeCaption: 'Выберите Время:',
      weekdays: [
        'Пн', 'Вт', 'Ср', 'Чт', 'Пт', 'Сб', 'Вс'
      ],
      months: [
        'Январь', 'Февраль', 'Март', 'Апрель',
        'Май', 'Июнь', 'Июль', 'Август',
        'Сентябрь', 'Октябрь', 'Ноябрь', 'Декабрь'
      ],
      graph: null,
    }
  },
  watch: {
    date: function(val) {
      if(val === ""){
        //reset
        this.dob = null,
        this.leapYear = null,
        this.year = null,
        this.month = null,
        this.day = null,
        this.yang = null,
        this.yin = null,
        this.intuition = null,
        this.logic = null,
        this.want = null,
        this.can = null,
        this.sex = null,
        this.sum = null,
        this.preFinalA = null,
        this.FinalA = null,
        this.phys = null,
        this.emotion = null,
        this.intel = null,
        this.table4Result = null,
        this.graph = null,
        this.we = null,
        this.iam = null;
        return 0;
      }
      this.dob = this.$moment(val);
      this.leapYear = this.dob.isLeapYear();
      this.year = this.dob.year();
      this.month = this.dob.month() + 1;
      this.day = this.dob.date();

      //get table data
      //calc month for leap year cases
      let tableM =
        this.month === 1 && this.leapYear === true
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

      //iam we
      let iam = table4Result[1];
      let we = table4Result[2];
      this.iam = iam;
      this.we = we;

      //get yin/yang
      let t3aN = table3aResult[0].split("-");
      let t3bN = table3bResult[0].split("-");
      let t3cN = table3cResult[0].split("-");

      let yang = parseInt(t3aN[1]) + parseInt(t3bN[0]) + parseInt(t3bN[1]);
      let yin = parseInt(t3aN[0]) + parseInt(t3cN[0]) + parseInt(t3cN[1]);

      this.yang = yang;
      this.yin = yin;

      //getting types

      this.phys = table3aResult[1];
      this.emotion = table3bResult[1];
      this.intel = table3cResult[1];

      //get graph

      this.graph = [
          {color:"purple", value:parseInt(t3cN[1]), name:'Аджна'},
          {color:"blue", value:parseInt(t3cN[0]), name:'Вишудха'},
          {color:"green", value:parseInt(t3bN[1]), name:'Анахата'},
          {color:"brown", value:parseInt(t3bN[0]), name:'Манипура'},
          {color:"orange", value:parseInt(t3aN[1]), name:'Свадхистана'},
          {color:"red", value:parseInt(t3aN[0]), name:'Муладхара'}
        ];

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
        preFinalA[2].toString().length === 5 ? fAfinal.toString().substr(1) : fAfinal.toString()
      ];

      this.FinalA = FinalA;
      this.table4Result = table4Result;

    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
$titleColor: #0884af;
$sizeB1: 24px;
$sizeB2: 22px;
$sizeB3: 20px;
$sizeB4: 18px;
.titleColor{
  color: $titleColor;
}
.calendar{
  font-family: sans-serif;
}
.group-title{
  color: $titleColor;
  font-weight: bold;
  text-transform: uppercase;
  font-size: $sizeB1;
  margin: 10px 0;
  margin-bottom: 10px;
}
h2,h3,label{
  margin-bottom: 0px;
}
  .container{
    margin-bottom: 50px;
  }
  .calendar-icon{
    height: 36px;
    padding-top: 15px;
  }
  .text-title{
    font-size: $sizeB4;
    display: flex;
    align-items: center;
    line-height: 16px;
    margin-bottom: 8px;
    .outlines-title{
      display: inline-block;
      text-align: right;
      width: 140px;
    }
    .outlines{
      display: inline-block;
      width: 185px;
      text-align: center;
      margin-left: 10px;
    }
  }
  .text-value{
    margin-top: 5px;
    margin-bottom: 50px;
    font-style: italic;
    font-weight: bold;
    line-height: 16px;
    font-size: $sizeB4;
    padding: 0;
  }
  .svg-inline--fa{
    margin-right: 5px;
  }
  .underline{
    &.fate-code-title{
      padding: 0 0 2px;
    }
    padding: 0 10px 2px;
    border-bottom: 1px solid $titleColor;
  }
  .red{
    color: #e23434 !important;
  }
  .purple{
    color: #cc129c !important;
  }
  .green{
    color: #44b747 !important;
  }
  .blue{
    color: #1d7ad6 !important;
  }
  .brown{
    color: #cc9019 !important;
  }
  .orange{
    color: #f46c0f !important;
  }
  .fate-code-title{
    b:nth-of-type(1){
      margin-left: 10px;
      margin-right: 7px;
    }
    b:nth-of-type(2){
      margin-left: 5px;
      margin-right: 14px;
    }
    b:nth-of-type(3){
      margin-left: 0px;
      margin-right: 16px;
    }
    font-size: $sizeB4;
  }
  .spaced-text{
    letter-spacing: 2px;
  }
  .font-size-numbers{
    font-size: $sizeB2;
  }
  .move-up{
    margin-top: -7px;
  }
  .smaller-font{
    font-size: $sizeB4;
  }
  .bold{
    font-weight: bold;
  }
  .yoga-bg:after{
    content: '';
    display: block;
    position: absolute;
    top: -15px;
    left: -115px;
    background-image: url('~@/assets/img/yoga-bg.png');
    background-size: contain;
    background-repeat: no-repeat;
    background-position: center;
    height: 305px;
    width: 100%;
    z-index: 0;
    opacity: 0.7;
  }
  .centered-box{
    line-height: $sizeB3;
    padding: 0 20px;
    width: 100%;
    max-width: 410px;
    margin: auto;
    text-align: left;
    .addon-title{
      text-transform: uppercase;
      font-size: $sizeB3;
      width: auto;
      margin-right: 5px;
      display: inline-block;
      z-index: 1;
      &.xl-longer{
        width: 100%;
        text-align: center;
      }
    }
    .addon-title.float-left{
      .name{
        //width: 70px;
        display: inline-block;
        text-align: right;
        margin-right: 10px;
        &.want{
          margin-right: 13px;
        }
      }
    }
    .addon-title.float-right{
      .name{
        //width: 150px;
        display: inline-block;
        text-align: right;
      }
      span:nth-of-type(2){
        display: inline-block;
        margin-left: 10px;
        width: 20px;
        text-align: left;;
      }
    }
    .move-right{
      margin-right: 20px !important;
    }
    .m-right{
      margin-right: 30px !important;
    }
    .m-left{
      margin-left: 30px !important;
      &.we-val{
        margin-left: 32px !important;
        &.more{
          margin-left: 42px !important;
        }
      }
    }
    .black-value{
      text-align: center;
      //width: 100px;
      margin-right: 5px;
      display: inline-block;
      color: #000;
      font-weight: bold;
      &.name, &.orange{
        margin-right: 0;
      }
      &.green{
        margin-left: 5px;
      }
      &.to-left{
        text-align: left;
      }
    }
    span span.black-value{
      display: inline;
    }
  }
  .yoga-bg{
    p{
      text-transform: uppercase;
      border-bottom: 1px solid $titleColor;
      text-align: right;
      font-size: $sizeB4;
      font-weight: bold;
    }
    z-index: 1;
    max-width: 410px;
    margin: auto;
  }
  .space-top{
    margin-top: 40px;
  }
  .year{
    text-transform: uppercase;
    font-size: $sizeB3;
    z-index: 20;
  }
  .space-bot{
    margin-bottom: 20px;
  }
  .bg-bot:before, .bg-bot:after{
    content: '';
    display: block;
    position: absolute;
    top: -40px;
    left: 0;
    background-image: url('~@/assets/img/bg-bot-left.png');
    background-size: contain;
    background-repeat: no-repeat;
    height: 170px;
    width: 100%;
    z-index: 1;
    opacity: 0.6;
  }
  .bg-bot:after{
    background-image: url('~@/assets/img/bg-bot-right.png');
    right: -20px;
    top: -138px;
    left: initial;
    width: 200px;
    height: 250px;
  }
  .add-space:before{
    content: '';
    width: 11px;
    display: inline-block;
  }
</style>