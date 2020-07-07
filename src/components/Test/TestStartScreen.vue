<template>
  <test-wrapper>
    <Header />
    <div class="test__body">
      <div class="test__prizes">
        <img class="test__prizes-image" src="/img/group-prize.png" alt="prizes image">
      </div>
    </div>
    <footer>
      <footer class="footer">
        <button class="test__control" type="button" @click="$emit('next', 'start')">
          дальше
        </button>
      </footer>
    </footer>
  </test-wrapper>
</template>

<script>
import TestWrapper from './TestWrapper';
import Header from './Header';

export default {
  name: 'TestStart',
  components: {
    Header,
    TestWrapper,
  },
};
</script>

<style scoped>
.test__prizes {
  display: grid;
  height: 100%;
}
.test__prizes-image {
  align-self: center;
  width: 100%;
}
</style>