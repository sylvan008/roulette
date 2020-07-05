<template>
  <div :class="['winners', isLightTheme ? 'winners--light' : '']">
    <ul class="winners__list">
      <li
        v-for="winner of winnersList"
        :key="winner.name"
        class="winners__item">
        <p class="winners__text">
          {{ winner.name }}
          <span class="winners__text--small">{{ winner.spins }} вращения</span>
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
            :src="`/img/prize-mini/${winner.prizeImage}`"
            :alt="`${winner.prize} prize image`"
            class="prize-image">
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
    },
    isLightTheme: {
      type: Boolean,
      default: false,
    },
    winnersLength: {
      type: Number,
      default: 3,
    },
    flipInterval: {
      type: Number,
      default: 2000,
    },
  },
  data() {
    return {
      winnersList: [],
      interval: null,
    };
  },
  mounted() {
    this.getRandomItems(this.winnersLength, this.winners);
    this.interval = this.createFlipInterval(this.flipInterval);
  },
  destroyed() {
    clearInterval(this.interval);
  },
  methods: {
    randomIndex(winnersCount) {
      return Math.floor(Math.random() * winnersCount);
    },
    getRandomItems(itemCount, winners) {
      this.winnersList.shift();
      const result = new Set(this.winnersList);
      while (result.size < itemCount) {
        const randomItem = winners[this.randomIndex(winners.length)];
        result.add(randomItem);
      }
      this.winnersList = [...result];
    },
    createFlipInterval(delay) {
      return setInterval(() => {
        this.getRandomItems(this.winnersLength, this.winners);
      }, delay);
    }
  },
};
</script>

<style scoped>
.winners--light {
  --background-color: #907EFF;
  --text-color: #FFFFFF;
  --image-mask: #907EFF;
}

/* Winners */
.winners {
  position: relative;
  overflow-y: hidden;
  border-radius: 21px;
  color: var(--text-color, #96B9FF);
  line-height: 1.1;
  background-color: var(--background-color, #18004C);
}
@media (min-width: 600px) {
  .winners {
    height: 220px;
    padding: 26px 10%;
  }
}

@media (max-width: 599.99px) {
  .winners {
    height: 150px;
    padding: 12px 3%;

  }
}

.winners:before {
  content: "";
  display: block;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: linear-gradient(180deg, rgba(150, 185, 255, 0.2) 0%, rgba(24, 0, 76, 0.5) 100%);
}

.winners__list {
  margin: 0;
  padding: 0;
  list-style: none;
}

.winners__item {
  margin-bottom: 19px;
  padding-left: 5px;
  padding-right: 5px;
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
}

/* Winners Text */
.winners__text {
  margin: 0;
  display: flex;
  flex: 0 0 40%;
  flex-direction: column;
}

@media (min-width: 600px) {
  .winners__text {
    font-size: 26px;
  }
}

@media (max-width: 599.99px) {
  .winners__text {
    font-size: 16px;
  }
}

/* Winners Text Small*/
.winners__text--small {}

@media (min-width: 600px) {
  .winners__text--small {
    font-size: 15px;
  }
}

@media (max-width: 599.99px) {
  .winners__text--small {
    font-size: 12px;
  }
}

/* Winners Prize Image */
.winners__prize-image {
  position: relative;
  line-height: 0;
  flex: 1 0 auto;
}

@media (min-width: 600px) {
  .winners__prize-image {
    height: 80px;
    max-width: 80px;
  }
}

@media (max-width: 599.99px) {
  .winners__prize-image {
    height: 50px;
    max-width: 50px;
  }
}


.prize-image {
  height: 100%;
}

.winners__prize-image:before {
  content: "";
  display: block;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: linear-gradient(0deg, var(--image-mask, #18004C) 0%, rgba(255, 255, 255, 0) 100%);
}
</style>