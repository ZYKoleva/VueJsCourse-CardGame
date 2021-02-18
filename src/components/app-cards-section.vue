<template>
    <section class="memory-game">
      <!-- <div
        class="memory-card"
        v-for="(card, index) in list_cards"
        :key="index"
        :data-framework="card.framework"
        @click="cardIsClicked(index)"
      >
        <img
          class="front-face"
          v-show="card.frontVisible"
          :src="card.imageFrontFace"
          alt="Aurelia"
        />
        <img
          class="back-face"
          v-show="card.backVisible"
          :src="card.imageBackFace"
          alt="JS Badge"
        />
      </div> -->
      <appCard class="memory-card"
        v-for="(card, index) in list_cards"
        :key="index" 
        :card = "card"
        :index = "index"
        @cardIsClicked = cardIsClicked($event)
        />
    </section>
</template>
<script>
import appCard from './app-card.vue'
export default {
    name: 'appGameSection',
    components: {
        appCard
    },
    props: {
        list_cards: Array,

    },
    methods: {
        cardIsClicked(index){
            this.$emit('cardIsClicked', index)
        },
    }
}
</script>

<style>
.memory-game {
  width: 640px;
  height: 640px;
  margin: auto;
  display: flex;
  flex-wrap: wrap;
  perspective: 1000px;
}

.memory-card {
  width: calc(25% - 10px);
  height: calc(33.333% - 10px);
  margin: 5px;
  position: relative;
  transform: scale(1);
  transform-style: preserve-3d;
  transition: transform 0.5s;
  box-shadow: 1px 1px 1px rgba(0, 0, 0, 0.3);
}

.disable-card {
  pointer-events: none;
}

.memory-card:active {
  transform: scale(0.97);
  transition: transform 0.2s;
}

.memory-card.flip {
  transform: rotateY(180deg);
}

.front-face,
.back-face {
  width: 100%;
  height: 100%;
  padding: 20px;
  position: absolute;
  border-radius: 5px;
  background: #fff29e;
}

.front-face {
  transform: rotateY(180deg);
}
</style>