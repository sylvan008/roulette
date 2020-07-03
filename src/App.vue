<template>
  <div id="app">
    <div class="container">
      <winners-ribbon :winners="winners"/>
    </div>
  </div>
</template>

<script>
import WinnersRibbon from './components/WinnersRibbon';
import winners from './assets/winners.json';

export default {
  name: 'App',
  components: {
    WinnersRibbon,
  },
  data() {
    return {
      winners,
    };
  },
}
</script>

<style>
.container {
  max-width: 570px;
  margin: 30px auto;
}
</style>
