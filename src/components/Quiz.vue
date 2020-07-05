<template>
  <div class="quiz">
    <div class="question">
      <p class="question__text">
        {{ question.text }}
      </p>
    </div>
    <answer-list
      :answers="question.answers"
      :answer-state="answerState"
      @answer="answerHandler"/>
  </div>
</template>

<script>
import AnswerList from './AnswerList';

export default {
  name: 'Quiz',
  components: {
    AnswerList,
  },
  props: {
    question: {
      type: Object,
      required: true,
    },
    answerState: {
      type: Object,
      default: null,
    }
  },
  methods: {
    answerHandler(answerId) {
      this.$emit('answer', answerId);
    },
  },
};
</script>

<style scoped>
/* Question Text */
.question__text {
  margin-top: 10px;
  line-height: 1.1;
  color: #300057;
}
@media (min-width: 600px) {
  .question__text {
    font-size: 47px;
  }
}
@media (max-width: 599.99px) {
  .question__text {
    font-size: 26px;
  }
}
</style>