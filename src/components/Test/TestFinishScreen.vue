<template>
  <test-wrapper>
    <header class="header-finish">
      <div class="prize-description">
        <p class="prize-description__title">ваш приз:</p>
        <h2 class="prize-description__name">{{ prize.name }}</h2>
      </div>
      <div class="prize-image">
        <img :src="`./img/prizes/${prize.image}`" :alt="`prize image ${prize.name}`">
      </div>
    </header>
    <div class="test-body">
      <div class="congratulation">
        <div class="congratulation__image">
          <div class="image-wrapper">
            <img :src="'./img/smile.png'" alt="congratulation image">
          </div>
        </div>
        <p class="congratulation__title">Молодец!</p>
        <p class="congratulation__text">
          {{ congratulationText }}
        </p>
      </div>
    </div>
    <footer class="footer">
      <a :href="externalLink" class="external-link test__control">забрать приз</a>
    </footer>
  </test-wrapper>
</template>

<script>
import TestWrapper from './TestWrapper';

export default {
  name: 'TestFinishScreen',
  components: {
    TestWrapper,
  },
  props: {
    externalLink: {
      type: String,
      required: true,
      default: '#',
    },
    prize: {
      type: Object,
      required: true,
    },
    testResult: {
      type: Number,
      default: 0,
    },
  },
  computed: {
    congratulationText() {
      switch (this.testResult) {
        case 4:
          return 'Ты отлично справился, нажми на кнопку ниже и забери свой приз';
        default:
          return 'Ты немного ошибся, но все равно справился, нажми на кнопку ниже и забери свой приз';
      }
    }
  }
};
</script>

<style scoped>
.header-finish {
  position: relative;
}

.external-link {
  text-decoration: none;
}

.prize-image {
}

.prize-image img {
  position: absolute;
  max-width: 130px;
  width: 100%;
  top: -55px;
  right: -45px;
}

/* Prize Description Title */
.prize-description__title {
  margin-top: 0;
  margin-bottom: 10px;
  color: #FFFFFF;
  text-transform: uppercase;
}
@media (max-width: 599.99px){
  .prize-description__title {
    font-size: 1.1rem;
  }
}

/* Prize Description Name */
.prize-description__name {
  margin: 0;
  font-weight: 600;
  color: #1C0057;
  text-transform: uppercase;
  white-space: nowrap;
}
@media (max-width: 599.99px) {
  .prize-description__name {
    font-size: 1.4rem;
  }
}

/* Congratulation */
.congratulation {
  max-width: 80%;
  margin: 60px auto 0;
  display: grid;
  align-items: center;
  text-align: center;
}

/* Congratulation Image */
.congratulation__image {
  display: flex;
  justify-content: center;
}
.congratulation__image img {
  width: 80px;
}

/* Congratulation Title*/
.congratulation__title {
  margin-top: 1rem;
  margin-bottom: 1rem;
  font-weight: 600;
  color: #1C0057;
  text-transform: uppercase;
}
@media (max-width: 599.99px) {
  .congratulation__title {
    font-size: 1.4rem;
  }
}
/* Congratulation Text */
.congratulation__text {
  margin: 0;
  color: #300057;
}
@media (max-width: 599.99px) {
  .congratulation__text {
    font-size: 1rem;
  }
}
</style>