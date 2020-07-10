<template>
  <div class="roulette-screen">
        <ul :class="rouletteClasses">
          <li v-for="(prize, index) of prizes" :key="index + 1" class="roulette-item"></li>
        </ul>
    <div class="roulette__controls">
      <button
        class="roulette__button"
        type="button"
        @click="rotationRoulette">
        крутить
      </button>
    </div>
  </div>
</template>

<script>
import { randomIndex } from '../helpers';

export default {
  name: 'Roulette',
  props: {
    maxRotations: {
      type: Number,
      default: 3,
    },
    prizes: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      currentRotation: 0,
      currentPrizeIndex: -1,
    };
  },
  computed: {
    rotationMoreIndexes() {
      return this.prizes.reduce((acc, prize, index) => {
        if (prize.isRotationMore) {
          acc.push(index);
        }
        return acc;
      }, []);
    },
    targetPrizeIndex() {
      return this.prizes.findIndex(prize => prize.isTargetPrize);
    },
    rouletteClasses() {
      return ['roulette', this.currentPrizeIndex !== -1 ? `number-${this.currentPrizeIndex + 1}` : ''];
    },
  },
  methods: {
    rotationRoulette() {
      this.currentRotation++;
      if (this.currentRotation < this.maxRotations) {
        const freeFields = this.rotationMoreIndexes.filter(num => num !== this.currentPrizeIndex);
        this.currentPrizeIndex = this.rotationMoreIndexes[randomIndex(freeFields.length)];
      } else {
        this.currentPrizeIndex = this.targetPrizeIndex;
      }
    },
  },
};
</script>

<style lang="scss">
  .roulette {
    width: 308px;
    height: 308px;
    padding: 0;
    margin: 0;
    position: relative;
    border-radius: 50%;
    overflow: hidden;
    counter-reset: num;
    background:
      center / contain no-repeat url("../../public/img/roulette-table.png"),
      center / contain no-repeat url("../../public/img/roulette-field.png");
    animation-timing-function: cubic-bezier(0,.4,.4,1.04);
    animation-duration: 3s;
    animation-fill-mode: forwards;
    animation-iteration-count: 1;
    &:after {
      content: "";
      display: block;
      width: 30px;
      height: 30px;
      background-image: linear-gradient(to bottom, #E0C560, #FFFFFF, #E0C560);
      border-radius: 50%;
      margin: auto;
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;
      position: absolute;
      box-shadow: 0 0 21px rgba(0, 0, 0, 0.25);
    }

    @for $i from 1 through 8 {
      &.number-#{$i} {
        animation-name: 'number-#{$i}';
      }
    }
  }

  .roulette-item {
    top: 0;
    right: 0;
    left: 0;
    margin: auto;
    position: absolute;
    display: block;
    width: 120px;
    height: 154px;
    transform-origin: 60px 154px;

    @for $i from 1 through 8 {
      &:nth-of-type(#{$i}) {
        transform: rotate(#{$i * 45deg});
      }
    }
  }

  @for $d from 1 through 8 {
    @keyframes number-#{$d} {
      from {
        transform: rotate(0);
      }
      to {
        transform: rotate(#{360 * 7 - 45 * $d}deg);
      }
    }
  }

  .roulette__controls {
    display: flex;
    justify-content: center;
  }
  .roulette__button {
    background-color: #0051EF;
    color: #FFFFFF;
    font-size: 1rem;
    text-transform: uppercase;
    border-radius: 1rem;
    border: none;

  }
</style>