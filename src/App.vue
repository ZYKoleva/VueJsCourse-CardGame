<template>
  <div id="app">
    <appButtons 
      :isWatchedStopped = 'isWatchedStopped'
      :counter = 'counter'
      :timeOutMessage = 'timeOutMessage'
      :noClickAllowed = 'noClickAllowed'
      @shuffleCards = shuffleCards()
      @startCounter = startCounter()
      @clearTimer = clearTimer()    
    />
    <appCardSection 
      :list_cards = 'list_cards'
      @cardIsClicked = cardIsClicked($event)
    />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import appButtons from './components/app-buttons.vue'
import appCardSection from './components/app-cards-section.vue'
let cards = [
  {
    hasMatch: false,
    frontVisible: false,
    backVisible: true,
    imageFrontFace: require("./assets/img/aurelia.svg"),
    imageBackFace: require("./assets/img/js-badge.svg"),
    framework: "aurelia",
  },
  {
    hasMatch: false,
    frontVisible: false,
    backVisible: true,
    imageFrontFace: require("./assets/img/vue.svg"),
    imageBackFace: require("./assets/img/js-badge.svg"),
    framework: "vue",
  },
  {
    hasMatch: false,
    frontVisible: false,
    backVisible: true,
    imageFrontFace: require("./assets/img/ember.svg"),
    imageBackFace: require("./assets/img/js-badge.svg"),
    framework: "ember",
  },
  {
    hasMatch: false,
    frontVisible: false,
    backVisible: true,
    imageFrontFace: require("./assets/img/backbone.svg"),
    imageBackFace: require("./assets/img/js-badge.svg"),
    framework: "backbone",
  },
  {
    hasMatch: false,
    frontVisible: false,
    backVisible: true,
    imageFrontFace: require("./assets/img/react.svg"),
    imageBackFace: require("./assets/img/js-badge.svg"),
    framework: "react",
  },
  {
    hasMatch: false,
    frontVisible: false,
    backVisible: true,
    imageFrontFace: require("./assets/img/angular.svg"),
    imageBackFace: require("./assets/img/js-badge.svg"),
    framework: "angular",
  },
  {
    hasMatch: false,
    frontVisible: false,
    backVisible: true,
    imageFrontFace: require("./assets/img/aurelia.svg"),
    imageBackFace: require("./assets/img/js-badge.svg"),
    framework: "aurelia",
  },
  {
    hasMatch: false,
    frontVisible: false,
    backVisible: true,
    imageFrontFace: require("./assets/img/vue.svg"),
    imageBackFace: require("./assets/img/js-badge.svg"),
    framework: "vue",
  },
  {
    hasMatch: false,
    frontVisible: false,
    backVisible: true,
    imageFrontFace: require("./assets/img/ember.svg"),
    imageBackFace: require("./assets/img/js-badge.svg"),
    framework: "ember",
  },
  {
    hasMatch: false,
    frontVisible: false,
    backVisible: true,
    imageFrontFace: require("./assets/img/backbone.svg"),
    imageBackFace: require("./assets/img/js-badge.svg"),
    framework: "backbone",
  },
  {
    hasMatch: false,
    frontVisible: false,
    backVisible: true,
    imageFrontFace: require("./assets/img/react.svg"),
    imageBackFace: require("./assets/img/js-badge.svg"),
    framework: "react",
  },
  {
    hasMatch: false,
    frontVisible: false,
    backVisible: true,
    imageFrontFace: require("./assets/img/angular.svg"),
    imageBackFace: require("./assets/img/js-badge.svg"),
    framework: "angular",
  },
];
let interval;
export default {
  name: "App",
  components: {
    appButtons,
    appCardSection,
  },
  data() {
    return {
      counter: 60,
      isWatchedStopped: false,
      timeOutMessage: "Your time is out!",
      noClickAllowed: "",
      list_cards: [...cards],
    };
  },
  watch: {
    counter: function(){
      if(this.counter === 0) {
        this.isWatchedStopped = true;
        this.clearTimer()

      }
    }
  },
  methods: {
    shuffleCards: function () {
      this.isWatchedStopped = false;
      this.noClickAllowed = "";
      this.list_cards = [...cards];
      let length_list_cards = this.list_cards.length;
      for (let i = 0; i < length_list_cards; i++) {
        let index1 = Math.floor(Math.random() * length_list_cards);
        let index2 = Math.floor(Math.random() * length_list_cards);
        let el1 = this.list_cards[index1];
        let el2 = this.list_cards[index2];
        this.list_cards[index2] = el1;
        this.list_cards[index1] = el2;
      }
      this.list_cards.forEach((card) => {
        card.hasMatch = false;
        card.frontVisible = false;
        card.backVisible = true;
      });
    },
    startCounter() {
      this.counter = 60;
      interval = setInterval(() => {
        this.counter -= 1;
      }, 1000);
    },
    clearTimer() {
      clearInterval(interval);
    },
    allCardsMatched(){
      let unmatched_cards_num = this.list_cards.filter(card => card.hasMatch === false).length;
      if(unmatched_cards_num === 0){
        this.clearTimer();
        this.isWatchedStopped = true;

      }
    },
    cardIsClicked: function (index) {
      if(this.counter > 0) {
         let current_card = this.list_cards[index];
      let opened_card = this.list_cards.filter(
        (card) => card.hasMatch === false && card.frontVisible === true
      )[0];
      if (opened_card) {
        if (current_card.framework === opened_card.framework) {
          current_card.hasMatch = true;
          opened_card.hasMatch = true;
          current_card.frontVisible = true;
          current_card.backVisible = false;
          this.allCardsMatched();
        } else {
          current_card.frontVisible = true;
          current_card.backVisible = false;
          opened_card.backVisible = true;
          opened_card.frontVisible = false;
        }
      } else {
        current_card.frontVisible = true;
        current_card.backVisible = false;
      }
    } else {
      this.noClickAllowed = "Please start again as this game has ended!"
    }
      },
     
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  height: 100vh;
  display: flex;
  background-image: linear-gradient(120deg, #d4fc79 0%, #96e6a1 100%);
}
#app {
  width: 100%;
  padding: 7%;
}


</style>

