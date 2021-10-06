<template>
  <div>
    <b-jumbotron>
      <template #header>New Quiz Game</template>

      <template #lead> Question : {{ currentQuestion.question }} </template>

      <hr class="my-4" />

      <p></p>

      <b-button variant="primary" href="#" @click="prev">Previous</b-button>
      <b-button variant="success" href="#" @click="next">Next</b-button>
    </b-jumbotron>
  </div>
</template>
<script>
export default {
  props: {
    currentQuestion: Object,
    prev: Function,
    next: Function,
  },
};
</script>
