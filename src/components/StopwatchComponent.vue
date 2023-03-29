<template>
  <div class="container">
    <Card v-for="(_, index) in cards" :key="index" :cardId="index"/>
    <div class="card add" @click="addCard">
      <svg width="20" height="20" viewBox="0 0 20 20" fill="#9E9E9E" xmlns="http://www.w3.org/2000/svg">
        <rect x="8.5" width="3" height="20" />
        <rect y="11.5" width="3" height="20" transform="rotate(-90 0 11.5)" />
      </svg>  
    </div>
  </div>
</template>

<script>
import Card from './CardComponent.vue'

export default {
  name: 'Stopwatch',
  components: {
    Card
  },
  data() {
    return {
      cards: []
    }
  },
  methods: {
    addCard() {
      this.cards.push({});
      setTimeout(() => {
        const newCardIndex = this.cards.length - 1;
        const newCard = this.$el.querySelector(`.card:nth-child(${newCardIndex + 1})`);
        newCard.classList.add('show');
      }, 50);
    }
  }
}
</script>

<style lang="scss">
  .container {
    margin: 72px 212px 0;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    column-gap: 10px;
    row-gap: 45px;

    @media (max-width: 1024px) {
      grid-template-columns: repeat(2, 1fr);
      margin: 72px 170px 0;
    }

    @media (max-width: 768px) {
      grid-template-columns: 1fr;
      margin: 72px 5% 0;
    }

  }

  .card {
    align-self: center;
    justify-self: center;
    width: 225px;
    height: 120px;
    background-color: #696969;
    position: relative;
    box-sizing: border-box;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
  }

  svg {
    cursor: pointer;
  }
  
  .add {
    cursor: pointer;
  }

  .show {
    animation: ani 1s;
  }

  @keyframes ani {
    from {
      opacity: 0;
      width: 0;
    }

    to {
      opacity: 1;
      width: 1fr;
    }
  }
</style>
