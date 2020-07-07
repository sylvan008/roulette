<template>
  <div id="app">
    <div class="app">
      <div class="app-vertical-position">
        <div class="app__test">
          <test :questions="questions" />
        </div>
      </div>
      <div class="dummy"></div>
      <div class="app__winners">
        <winners-ribbon
          :winners="winners"
          :flip-interval="3000"/>
      </div>
    </div>
  </div>
</template>

<script>
import winners from './assets/winners.json';
import questions from './assets/questions.json';
import WinnersRibbon from './components/WinnersRibbon';
import Test from './components/Test/Test';

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
.app {
  position: relative;
  height: 100vh;
  width: 100vw;
  display: grid;
  grid-template-rows: minmax(auto, 550px) 1fr 110px;
}
/* App Winners */
.app__winners  {
  max-width: 570px;
  margin: 0 auto;
  overflow-y: hidden;
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
  margin-left: 10%;
  margin-right: 10%;
  display: grid;
  height: 100%;
}
@media (min-width: 600px) {
  .app__test {
    max-width: 574px;
  }
}
.app-vertical-position {
  position: relative;
  margin-top: 10%;
}
</style>
