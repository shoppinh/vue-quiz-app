<template>
  <div>
    <b-container>
      <b-jumbotron>
        <template #header>New Quiz Game</template>

        <template #lead> Question : {{ currentQuestion.question }} </template>

        <hr class="my-4" />

        <h4>List of answers</h4>
        <b-list-group>
          <b-list-group-item
            v-for="(answer, index) in shuffledAnswers"
            :key="index"
            @click="selectAnswer(index)"
            :class="showAnswerClass(index)"
            >{{ answer }}</b-list-group-item
          >
        </b-list-group>

        <b-button variant="primary" href="#" @click="next">Next</b-button>
        <b-button
          variant="success"
          href="#"
          @click="submitAnswer"
          :disabled="selectedIndex === null || answered"
          >Submit</b-button
        >
      </b-jumbotron>
    </b-container>
  </div>
</template>
<script>
import _ from "lodash";
export default {
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function,
  },
  data() {
    return {
      selectedIndex: null,
      correctIndex: null,
      shuffledAnswers: [],
      answered: false,
    };
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
    },
    submitAnswer() {
      let isCorrect = false;
      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }
      this.increment(isCorrect);
      this.answered = true;
    },
    shuffleAnswer() {
      let answers = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer,
      ];
      this.shuffledAnswers = _.shuffle(answers);
      this.correctIndex = this.shuffledAnswers.indexOf(
        this.currentQuestion.correct_answer
      );
    },
    showAnswerClass(index) {
      let answerClass = "";
      if (!this.answered && this.selectedIndex === index) {
        answerClass = "selected";
      } else if (this.answered && this.correctIndex === index) {
        answerClass = "correct";
      } else if (
        this.answered &&
        this.selectedIndex === index &&
        this.correctIndex !== index
      ) {
        answerClass = "incorrect";
      }
      return answerClass;
    },
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.shuffleAnswer();
        this.answered = false;
      },
    },
  },
  computed: {},
};
</script>
<style scoped>
.list-group {
  margin-bottom: 15px;
}
.list-group-item:hover {
  background-color: #efefef;
  cursor: pointer;
}
.btn {
  margin: 0 5px;
}
.selected,
.selected:hover {
  background-color: lightblue;
}
.correct,
.correct:hover {
  background-color: green;
  color: white;
}
.incorrect,
.incorrect:hover {
  background-color: red;
  color: white;
}
</style>
