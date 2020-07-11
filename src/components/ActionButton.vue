<template>
  <button
    :class="stylesObject"
    type="button"
    v-on="$listeners">
    <slot />
  </button>
</template>

<script>
const LIGHT = 'light';
const DARK = 'dark';

export default {
  name: 'ActionButton',
  props: {
    themeType: {
      type: String,
      default: LIGHT,
    },
  },
  computed: {
    stylesObject() {
      const styles = ['action__button'];
      switch (this.themeType) {
        case LIGHT:
          styles.push(`action__button--${LIGHT}`);
          break;
        case DARK:
          styles.push(`action__button--${DARK}`);
          break;
      }
      return styles;
    },
  },
};
</script>

<style scoped>
  /* Test Control */
  .action__button {
    border: none;
    background: var(--background-color, #1C0057);
    color: #FFFFFF;
    line-height: 1.1;
    text-transform: uppercase;
  }
  @media (min-width: 600px) {
    .action__button {
      padding: 1rem 2.1rem;
      font-size: 3rem;
      border-radius: 3rem;
    }
  }
  @media (max-width: 599.99px) {
    .action__button {
      padding: 0.7rem 1.4rem;
      font-size: 1.4rem;
      border-radius: 1.4rem;
    }
  }
  .action__button--light {
    --background-color: #0051EF;
  }
</style>