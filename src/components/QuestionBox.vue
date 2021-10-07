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
            v-for="(answer, index) in answers"
            :key="index"
            @click="selectAnswer(index)"
            :class="[selectedIndex === index ? 'selected' : '']"
            >{{ answer }}</b-list-group-item
          >
        </b-list-group>

        <b-button variant="primary" href="#" @click="prev">Previous</b-button>
        <b-button variant="success" href="#" @click="next">Next</b-button>
      </b-jumbotron>
    </b-container>
  </div>
</template>
<script>
export default {
  props: {
    currentQuestion: Object,
    prev: Function,
    next: Function,
  },
  data() {
    return {
      selectedIndex: null,
    };
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
    },
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      return answers;
    },
  },
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
.correct {
  background-color: green;
}
.incorrect {
  background-color: red;
}
</style>
