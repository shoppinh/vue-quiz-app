<template>
  <div>
    <b-nav>
      <b-nav-item disabled>Question</b-nav-item>
      <b-nav-item disabled
        >Counter : {{ numOfCorrect }}/{{ questionLength }}</b-nav-item
      >
    </b-nav>
  </div>
</template>
<script>
export default {
  props: {
    questionLength: Number,
    numOfCorrect: Number,
  },
};
</script>
