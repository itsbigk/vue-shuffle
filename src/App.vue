<template>
  <div id="app">
    <div class="count-section">
      # of shuffles: {{ shuffleCount }}
    </div>
    <h1 class="title">
      <img class="vue-logo" src="./assets/logo.png" />
      Card Shuffling
    </h1>
    <div class="speed-buttons">
      <button v-for="type in shuffleTypes"
        class="button is-small"
        :class="{ 'is-light': shuffleSpeed !== `shuffle${type}` }"
        @click="shuffleSpeed = `shuffle${type}`">
        {{ type }}
      </button>
    </div>
    <div class="main-buttons">
      <button v-if="isDeckShuffled"
        class="button is-primary is-outlined"
        @click="displayInitialDeck">
        Reset <i class="fas fa-undo"></i>
      </button>
      <button @click="shuffleDeck" class="button is-primary">
        Shuffle <i class="fas fa-random"></i>
      </button>
    </div>
    <transition-group :name="shuffleSpeed" tag="div" class="deck">
      <Card
        v-for="card in cards"
        :key="card.id"
        :card="card"
      />
    </transition-group>
  </div>
</template>

<script>
  import Card from './components/Card'
  import shuffle from 'lodash/shuffle'

  export default {
    name: 'app',
    components: {
      Card
    },
    data () {
      return {
        ranks: ['A', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K'],
        suits: ['♥','♦','♠','♣'],
        cards: [],
        shuffleSpeed: 'shuffleMedium',
        shuffleTypes: ['Slow', 'Medium', 'Fast'],
        isDeckShuffled: false,
        shuffleCount: 0
      }
    },
    created () {
      this.displayInitialDeck()
    },
    methods: {
      displayInitialDeck () {
        const cardsWithoutIds = [].concat(
          ...this.suits.map(suit => this.ranks.map(rank => ({ suit, rank })))
        )

        this.cards = cardsWithoutIds.map((card, index) => ({ ...card, id: index + 1 }))
        this.isDeckShuffled = false
        this.shuffleCount = 0
      },
      shuffleDeck () {
        this.cards = shuffle(this.cards)
        this.isDeckShuffled = true
        this.shuffleCount++
      }
    }
  }
</script>

<style src="./styles/app.css"></style>
