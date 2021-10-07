<template>
  <div id="app">
    <Header :questionLength="questions.length" :numOfCorrect="numOfCorrect" />
    <QuestionBox
      v-if="questions.length"
      :currentQuestion="questions[index]"
      :next="next"
      :increment="increment"
    />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionBox.vue";

export default {
  name: "App",
  data() {
    return {
      questions: [],
      index: 0,
      numOfCorrect: 0,
    };
  },
  components: {
    Header,
    QuestionBox,
  },
  methods: {
    next: function() {
      if (this.index < this.questions.length) {
        this.index++;
      }
    },
    increment: function(isCorrect) {
      if (isCorrect) {
        this.numOfCorrect++;
      }
    },
  },
  mounted: function() {
    fetch("https://opentdb.com/api.php?amount=50&category=11")
      .then((response) => {
        return response.json();
      })
      .then((response) => {
        this.questions = response.results;
      });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
