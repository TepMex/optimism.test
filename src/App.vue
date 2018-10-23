<template>
  <div id="app">
    <p>Представьте, что с вами произошла описанная ситуация, и выберете более близкую вам реакцию. Не так, как "правильно", а так как вы обычно думаете!</p>
    <hr/>
    <Question v-if="dataLoaded && !showReport" 
    :question="this.currentQuestion.question" 
    :answer-a="this.currentQuestion.A.answer" 
    :answer-b="this.currentQuestion.B.answer"
    @answered="onAnswered" />
    <button v-if="!dataLoaded" @click="loadData()">НАЧАТЬ ТЕСТ</button>
    <Report :rdata="this.score" v-if="showReport" />
  </div>
</template>

<script>
import Question from "./components/Question.vue";
import Report from "./components/Report.vue";
import axios from "axios";

export default {
  name: "app",
  components: {
    Question,
    Report
  },

  data: () => ({
    dataLoaded: false,
    showReport: false,
    questions: [],
    currentQuestion: null,
    score: {
      PersonGood: 0,
      PersonBad: 0,
      GeneralGood: 0,
      GeneralBad: 0,
      PersistentGood: 0,
      PersistentBad: 0
    }
  }),

  methods: {
    nextQueston: function() {
      return this.questions.pop();
    },

    onAnswered: function(e) {
      let cls = this.currentQuestion.class;
      this.score[cls] += this.currentQuestion[e].score;
      if (this.questions.length) {
        this.currentQuestion = this.nextQueston();
      }
      else{
        this.showReport = true;
      }
    },

    prepareData: function(data) {
      return data.sort((a, b) => Math.random() - Math.random());
    },

    loadData: function() {
      axios
        .get("/data.json")
        .then(response => {
          this.questions = this.prepareData(response.data);
          this.currentQuestion = this.nextQueston();
          this.dataLoaded = true;
        })
        .catch(e => {
          console.error(e);
          this.dataLoaded = false;
        });
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
