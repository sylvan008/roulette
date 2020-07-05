<template>
  <div id="app">
    <div class="app">
      <div class="app__test">
        <test :questions="questions" />
      </div>
      <div class="app__winners">
        <winners-ribbon :winners="winners" />
      </div>
    </div>
  </div>
</template>

<script>
import winners from './assets/winners.json';
import questions from './assets/questions.json';
import WinnersRibbon from './components/WinnersRibbon';
import Test from './components/Test';

export default {
  name: 'App',
  components: {
    WinnersRibbon,
    Test,
  },
  data() {
    return {
      winners,
      questions,
    };
  },
}
</script>

<style>
/* App Winners */
.app__winners  {
  max-width: 570px;
  position: fixed;
  bottom: -30px;
  left: 50%;
  transform: translateX(-50%);
}
@media (min-width: 600px) {
  .app__winners {
    width: 100%;
  }
}
@media (max-width: 599.99px) {
  .app__winners {
    width: 80%;
  }
}

/* App Test */
.app__test {
  margin: 30px auto;
}
@media (min-width: 600px) {
  .app__test {
    max-width: 574px;
    width: 100%
  }
}
@media (max-width: 599.99px) {
  .app__test {
    width: 90%;
  }
}
</style>
