<template>
  <transition name="fade-in-screen" mode="out-in" class="test-screen-hide">
    <component
      :is="currentScreen"
      v-bind="currentScreenProps"
      @next="nextHandler"
      @test-result="testResultHandler"/>
  </transition>
</template>

<script>
import TestStartScreen from './TestStartScreen';
import TestingScreen from './TestingScreen';
import TestFinishScreen from './TestFinishScreen';

export default {
  name: 'Test',
  components: {
    TestStartScreen,
    TestingScreen,
    TestFinishScreen,
  },
  props: {
    questions: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      testState: 0,
      testResult: 0,
    };
  },
  computed: {
    currentScreen() {
      switch (this.testState) {
        case 0:
          return 'TestStartScreen';
        case 1:
          return 'TestingScreen';
        case 2:
          return 'TestFinishScreen';
      }
    },
    currentScreenProps() {
      switch (this.testState) {
        case 1:
          return {
            questions: this.questions
          };
        case 2:
          return {
            externalLink: '#',
            testResult: this.testResult,
            prize: {
              name: 'iPhone 11',
              image: 'ps-4.png',
            }
          }
      }
    },
  },
  methods: {
    nextHandler(e) {
      this.testState++;
      console.log(e);
    },
    testResultHandler(result) {
      const reducer = (acc, key) => result[key] === 'success' ? ++acc : acc;
      this.testResult = Object.keys(result).reduce(reducer, 0);
    },
  },
};
</script>

<style>
.test__body {
  margin-top: 1rem;
}

.footer {
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
    padding: 1rem 2.1rem;
    font-size: 3rem;
    border-radius: 3rem;
  }
}
@media (max-width: 599.99px) {
  .test__control {
    padding: 0.7rem 1.4rem;
    font-size: 1.4rem;
    border-radius: 1.4rem;
  }
}

.fade-in-screen-enter-active, .fade-in-screen-leave-active {
  transition: all 0.2s;
}
.fade-in-screen-leave-to {
  transform: scale(0.9) translateX(-120%);
}
.fade-in-screen-enter {
  transform: scale(0.9) translateX(100%);
}
.test-screen-hide:after  {
  content: "";
  position: absolute;
  top: 5%;
  height: 90%;
  width: 15px;
  transition: all 0.2s;
  background-color: #907EFF;
  left: 0;
  border-top-right-radius: 21px;
  border-bottom-right-radius: 21px;
}
</style>