<template>
    <table>
        <tr>
            <td>Устойчивость плохого</td>
            <td>{{rdata.PersistentBad}}</td>
            <td>{{this.gradeBad[rdata.PersistentBad]}}</td>
        </tr>
        <tr>
            <td>Устойчивость хорошего</td>
            <td>{{rdata.PersistentGood}}</td>
            <td>{{this.gradeGood[rdata.PersistentGood]}}</td>
        </tr>
        <tr>
            <td>Обобщение плохого</td>
            <td>{{rdata.GeneralBad}}</td>
            <td>{{this.gradeBad[rdata.GeneralBad]}}</td>
        </tr>
        <tr>
            <td>Обобщение  хорошего</td>
            <td>{{rdata.GeneralGood}}</td>
            <td>{{this.gradeGood[rdata.GeneralGood]}}</td>
        </tr>
        <tr>
            <td>Персонализация плохого</td>
            <td>{{rdata.PersonBad}}</td>
            <td>{{this.gradeSE[rdata.PersonBad]}}</td>
        </tr>
        <tr>
            <td>Персонализация хорошего</td>
            <td>{{rdata.PersonGood}}</td>
            <td>{{this.gradeGood[rdata.PersonGood]}}</td>
        </tr>
        <tr></tr>
        <tr>
            <td>Коэффициент надежды</td>
            <td>{{rdata.PersistentBad+rdata.GeneralBad}}</td>
            <td>{{this.gradeHope[rdata.PersistentBad+rdata.GeneralBad]}}</td>
        </tr>
        
        <tr>
            <td>ИТОГО ОПТИМИЗМ</td>
            <td>{{(rdata.GeneralGood+rdata.PersistentGood+rdata.PersonGood) - (rdata.GeneralBad+rdata.PersistentBad+rdata.PersonBad)}}</td>
            <td>{{this.checkOptimism((rdata.GeneralGood+rdata.PersistentGood+rdata.PersonGood) - (rdata.GeneralBad+rdata.PersistentBad+rdata.PersonBad))}}</td>
        </tr>

    </table>
</template>

<script>
export default {
  name: "Report",
  props: {
    rdata: Object
  },

  data: () => ({
    gradeBad: [
      "очень оптимистично",
      "очень оптимистично",
      "умеренно оптимистично",
      "умеренно оптимистично",
      "промежуточное значение",
      "скорее пессимистично",
      "скорее пессимистично",
      "пессимистично",
      "пессимистично"
    ],
    gradeGood: [
      "очень пессимистично",
      "очень пессимистично",
      "очень пессимистично",
      "умеренно пессимистично",
      "промежуточное значение",
      "промежуточное значение",
      "умеренно оптимистично",
      "очень оптимистично",
      "очень оптимистично"
    ],

    gradeHope: [
      "ваша надежда чрезвычайно сильна",
      "ваша надежда чрезвычайно сильна",
      "ваша надежда чрезвычайно сильна",
      "вы умеренно надеющийся",
      "вы умеренно надеющийся",
      "вы умеренно надеющийся",
      "вы умеренно надеющийся",
      "промежуточное значение",
      "промежуточное значение",
      "вы умеренно не надеющийся",
      "вы умеренно не надеющийся",
      "вы умеренно не надеющийся",
      "вы ни на что не надеетесь",
      "вы ни на что не надеетесь",
      "вы ни на что не надеетесь",
      "вы ни на что не надеетесь",
      "вы ни на что не надеетесь"
    ],

    gradeSE: [
      "очень высокая самооценка",
      "очень высокая самооценка",
      "умеренная самооценка",
      "умеренная самооценка",
      "промежуточный показатель самооценки",
      "умеренно низкая самооценка",
      "умеренно низкая самооценка",
      "очень низкая самооценка",
      "очень низкая самооценка"
    ]
  }),

  methods: {
    checkOptimism: function(score) {
      let result = "";
      if (score > 8) {
        result =
          "вы очень оптимистичны по отношению к широкому спектру событий";
      } else if (score > 5) {
        result =
          "вы умеренно оптимистичны";
      } else if (score > 2) {
        result =
          "нейтральное значение оптимизм/пессимизм";
      } else if (score > 0) {
        result =
          "вы умеренно пессимистичны";
      } else {
        result =
          "вы очень пессимистичны";
      }

      return result;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
