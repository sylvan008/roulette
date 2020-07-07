<template functional>
  <header class="header">
    <p class="header__motivation">Отвечай на вопросы викторины и</p>
    <h2 class="header__reward">выигрывай крутые призы</h2>
    <p class="header__motivation">Чтобы забрать приз ответьте на несколько вопросов:</p>
  </header>
</template>

<script>
export default {
  name: 'Header',
};
</script>

<style scoped>
/* Header Motivation */
.header__motivation {
  margin-top: 0;
  margin-bottom: 0.7rem;
  line-height: 1.1;
  color: #FFFFFF;
}
@media (min-width: 600px) {
  .header__motivation {
    font-size: 1.9rem;
  }
}
@media (max-width: 599.99px) {
  .header__motivation {
    font-size: 1rem;
  }
}

/* Header Reward */
.header__reward {
  margin-top: 0;
  margin-bottom: 1rem;
  font-weight: 600;
  line-height: 1.1;
  text-transform: uppercase;
  color: #1C0057;
}
@media (min-width: 600px) {
  .header__reward {
    font-size: 3rem;
  }
}
@media (max-width: 599.99px) {
  .header__reward {
    font-size: 1.4rem;
  }
}
</style>