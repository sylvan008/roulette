<template>
  <section class="test">
    <header class="header">
      <p class="header__motivation">Отвечай на вопросы викторины и</p>
      <h2 class="header__reward">выигрывай крутые призы</h2>
      <p class="header__motivation">Чтобы забрать приз ответьте на несколько вопросов:</p>
    </header>
    <div class="test__body">
      <div class="indicator">
        <div
          v-for="num in 4"
          :key="num"
          :class="['indicator-item', (num === questionNum) ? 'indicator-item--active' : '']"/>
      </div>
      <div class="question__number">&#8470;{{ questionNum }}</div>
      <quiz
        v-if="activeQuestion"
        :answerState="answerState"
        :question="activeQuestion"
        @answer="answerHandler"/>
    </div>
    <footer class="footer">
      <button class="test__control" type="button" @click="nextQuestion">дальше</button>
    </footer>
  </section>
</template>

<script>
import Quiz from './Quiz';

export default {
  name: 'Test',
  components: {
    Quiz,
  },
  props: {
    questions: {
      type: Array,
      default: () => [],
    },
    testLength: {
      type: Number,
      default: 4,
    },
  },
  data() {
    return {
      questionNum: 1,
      result: {},
      answerState: null,
    };
  },
  computed: {
    activeQuestion() {
      return this.questions[this.questionNum - 1];
    }
  },
  methods: {
    nextQuestion() {
      if (this.questionNum >= this.testLength) {
        return;
      }
      this.answerState = null;
      this.questionNum++;
    },
    answerHandler(answerId) {
      const SUCCESS = 'success';
      const FAIL = 'fail';
      const questionId = this.activeQuestion.id;
      const { rightAnswerId } = this.activeQuestion;
      if (rightAnswerId === answerId) {
        this.answerState = { [answerId]: SUCCESS };
        if (!this.result[questionId]) {
          this.result[questionId] = SUCCESS;
        }
      } else {
        this.answerState = { [answerId]: FAIL };
        if (!this.result[questionId]) {
          this.result[questionId] = FAIL;
        }
      }
    },
  },
};
</script>

<style scoped>
.test {
  padding: 18px 28px 42px 28px;
  background: #907EFF;
  box-shadow: 0px 0px 62px rgba(144, 126, 255, 0.39);
  border-radius: 21px;
}

.test__body {
  margin-top: 28px;
}

/* Header Motivation */
.header__motivation {
  margin-top: 0;
  margin-bottom: 12px;
  line-height: 1.1;
  color: #FFFFFF;
}
@media (min-width: 600px) {
  .header__motivation {
    font-size: 31px;
  }
}
@media (max-width: 599.99px) {
  .header__motivation {
    font-size: 18px;
  }
}

/* Header Reward */
.header__reward {
  margin-top: 0;
  margin-bottom: 20px;
  font-weight: 600;
  line-height: 1.1;
  text-transform: uppercase;
  color: #1C0057;
}
@media (min-width: 600px) {
  .header__reward {
    font-size: 47px;
  }
}
@media (max-width: 599.99px) {
  .header__reward {
    font-size: 26px;
  }
}

/* Question Number */
.question__number {
  margin-top: 18px;
  line-height: 1.1;
  color: #FFFFFF;
}
@media (min-width: 600px) {
  .question__number {
    font-size: 47px;
  }
}
@media (max-width: 599.99px) {
  .question__number {
    font-size: 26px;
  }
}

.footer {
  margin-top: 55px;
  margin-bottom: 43px;
  display: flex;
  justify-content: center;
}

/* Test Control */
.test__control {
  border: none;
  background: #1C0057;
  color: #FFFFFF;
  line-height: 1.1;
  text-transform: uppercase;
}
@media (min-width: 600px) {
  .test__control {
    padding: 16px 39px;
    font-size: 47px;
    border-radius: 45px;
  }
}
@media (max-width: 599.99px) {
  .test__control {
    padding: 12px 26px;
    font-size: 26px;
    border-radius: 26px;
  }
}

.indicator {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-column-gap: 5px;
}
.indicator-item {
  border: 3px solid rgba(255, 255, 255, 0.3);
  border-radius: 2px;
}
.indicator-item--active {
  border-color: #FFFFFF;
}
</style>