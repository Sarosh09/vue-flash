<template>
  <div id="app">
    <main class="page-container">
      <header class="page-header">
        <div class="top-message">
          <span class="text">
            <svg
              class="icon"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 50 50"
            >
              <path
                d="M24.85 10.126c2.018-4.783 6.628-8.125 11.99-8.125 7.223 0 12.425 6.179 13.079 13.543 0 0 .353 1.828-.424 5.119-1.058 4.482-3.545 8.464-6.898 11.503L24.85 48 7.402 32.165c-3.353-3.038-5.84-7.021-6.898-11.503-.777-3.291-.424-5.119-.424-5.119C.734 8.179 5.936 2 13.159 2c5.363 0 9.673 3.343 11.691 8.126z"
              />
            </svg>
            First Vue.js project |
            <a href="" target="_blank" rel="noopener noreferrer"
              >Mohammad Sarosh Basit</a
            >
          </span>
        </div>
        <!-- end of top message -->
        <h1 class="title">Simple Flashcard App</h1>
        <Search @searchTrigger="searchCards"></Search>
      </header>
      <!-- end of page header -->
      <AddNewCard @addCardTrigger="addCard"></AddNewCard>
      <p class="reviewcounter">You have reviewed {{ reviews }} cards so far</p>
      <ul class="cards-box">
        <Card
          v-for="card in filteredData"
          :key="card.id"
          :card="card"
          @reviewTrigger="recalculateReviews"
          @deleteTrigger="deleteCard"
        ></Card>
      </ul>
      <!-- end of cards box -->
    </main>
  </div>
</template>

<script>
import Search from './components/Search';
import AddNewCard from './components/AddNewCard';
import Card from './components/Card';

const uuidv4 = require('uuid/v4');
const colors = ['-orange', '-red', '-purple', '-blue', '-green'];

let cards = [
  {
    id: uuidv4(),
    front: 'Hindi for elephant?',
    back: 'Haathi',
    flipped: false,
    reviewed: true,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`,
  },
  {
    id: uuidv4(),
    front:
      'Hindi for cat?',
    back:
      'Billi',
    flipped: false,
    reviewed: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`,
  },
  {
    id: uuidv4(),
    front: 'Hindi for dog?',
    back: 'Kutta',
    flipped: false,
    reviewed: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`,
  },
  {
    id: uuidv4(),
    front: 'English for ullu?',
    back: 'Owl',
    flipped: false,
    reviewed: true,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`,
  },
  {
    id: uuidv4(),
    front: 'Tamil for cow?',
    back: 'Matu',
    flipped: false,
    reviewed: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`,
  },
  {
    id: uuidv4(),
    front: 'Kannada for cow?',
    back: "Hasu",
    flipped: false,
    reviwed: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`,
  },
  {
    id: uuidv4(),
    front: 'Gujrati for cow?',
    back: 'Gaya',
    flipped: false,
    reviewed: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`,
  },
  {
    id: uuidv4(),
    front: 'Who designed this app? ✏️',
    back: 'Such a modest boy...',
    flipped: false,
    reviewed: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`,
  },
];

export default {
  name: 'app',
  data() {
    return {
      cards: cards,
      searchWord: '',
      reviews: cards.filter((card) => card.reviewed).length,
    };
  },
  methods: {
    searchCards(keyword) {
      this.searchWord = keyword;
    },
    recalculateReviewes(value) {
      value ? this.reviews++ : this.reviews--;
    },
    deleteCard(id) {
      this.cards = this.cards.filter((card) => {
        if (card.id === id && card.reviewed) {
          this.reviews--;
        }
        return card.id !== id;
      });
    },
    addCard(data) {
      this.cards.unshift(data);
    },
  },
  computed: {
    filteredData() {
      return this.cards.filter((card) => {
        return card.front
          .toLowerCase()
          .includes(this.searchWord.trim().toLowerCase());
      });
    },
  },
  components: {
    Search,
    AddNewCard,
    Card,
  },
};
</script>

<style lang="sass">
@import './assets/sass/main.sass';

.page-container
  margin-left: auto
  margin-right: auto
  max-width: 1120px
  padding-top: 1.5rem
  padding-left: 1rem
  padding-right: 1rem
  overflow: hidden

.top-message
  font-size: 0.8571rem
  text-align: left
  color: $muted
  .text
    display: flex
    align-items: center
  .icon
    width: 20px
    fill: #ff4242
    margin-right: 9px

.page-header
  padding-bottom: 40px
  border-bottom: 1px dashed #dedede
  .title
    font-size: 2.286rem
    font-weight: $bold
    text-align: center
    margin-top: 3.5rem
    margin-bottom: 3rem

.reviewcounter
  font-size: 1.143rem
  font-weight: $bold

.cards-box
  margin-top: 1rem
  margin-left: -1.5rem
  margin-right: -1.5rem
  display: flex
  flex-wrap: wrap
  justify-content: center
</style>
