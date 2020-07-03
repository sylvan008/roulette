<template>
  <div class="winners">
    <ul class="winners__list">
      <li
        v-for="winner of winners"
        :key="winner.name"
        class="winners__item">
        <p class="winners__text">
          {{ winner.name }}
          <span class="winners__text--small">{{ winner.spin }} вращения</span>
        </p>
        <p class="winners__text">
          <span class="winners__text--small">Приз:</span>
          <span>
            {{ winner.prizeName }}
            <span v-if="winner.prizeAnnex" class="winners__text--small">
              {{ winner.prizeAnnex }}
            </span>
          </span>
        </p>
        <div class="winners__prize-image">
          <img
            :src="`/img/${winner.prizeImage}`"
            :alt="`${winner.prize} prize image`">
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'WinnersRibbon',
  props: {
    winners: {
      type: Array,
      default: () => [],
    }
  }
};
</script>

<style scoped>
.winners {
  padding: 26px 60px;
  border-radius: 21px;
  color: #96B9FF;
  line-height: 1.1;
  background-color: #18004C;
}

.winners__list {
  margin: 0;
  padding: 0;
  list-style: none;
}

.winners__item {
  margin-bottom: 6px;
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
}

.winners__text {
  margin: 0;
  display: flex;
  flex: 0 0 40%;
  flex-direction: column;
  font-size: 26px;
}

.winners__text--small {
  font-size: 15px;
}

.winners__prize-image img {
  max-width: 80px;
}
</style>