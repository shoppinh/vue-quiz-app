<template>
  <div id="app">
    <Header :questionLength="questions.length" :index="index" />
    <QuestionBox
      v-if="questions.length"
      :currentQuestion="questions[index]"
      :next="next"
      :prev="prev"
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
    };
  },
  components: {
    Header,
    QuestionBox,
  },
  methods: {
    next: function() {
      this.index++;
    },
    prev: function() {
      if (this.index > 0) {
        this.index--;
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
