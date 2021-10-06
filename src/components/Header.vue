<template>
  <div>
    <b-nav>
      <b-nav-item disabled>Question</b-nav-item>
      <b-nav-item disabled>{{ index + 1 }}/{{ questionLength }}</b-nav-item>
    </b-nav>
  </div>
</template>
<script>
export default {
  props: {
    questionLength: Number,
    index: Number,
  },
};
</script>
