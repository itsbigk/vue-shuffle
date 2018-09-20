<template>
  <div class="card"
    :class="suitColor[card.suit]">
      <span class="card__suit card__suit--top">{{ card.suit }}</span>
      <span class="card__number">{{ card.rank }}</span>
      <span class="card__suit card__suit--bottom">{{ card.suit }}</span>
  </div>
</template>

<script>
  export default {
    name: 'Card',
    props: {
      card: Object
    },
    data () {
      return {
        suitColor: {
          '♠': 'black',
          '♣': 'black',
          '♦': 'red',
          '♥': 'red',
        }
      }
    }
  }
</script>

<style src="../styles/card.css"></style>
