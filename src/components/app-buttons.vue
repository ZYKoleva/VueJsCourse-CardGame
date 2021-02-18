<template>
        <div class="counter-shuffle-btn-wrapper">
      <button class="shuffle-btn" @click="shuffleCards(), startCounter()">
        Shuffle Cards
      </button>
      <button class="stop-timer-btn" @click="clearTimer()">Stop Timer</button>
      <div class="counter">
        <h1>
          <span v-show="counter > 0 && !isWatchedStopped">{{ counter }}</span>
          
          <span v-show="counter === 0">{{ timeOutMessage }}</span>
          <span v-if="counter > 0 && isWatchedStopped">You Won!!! It took you only {{ counter }} seconds.</span>
        </h1>
        <p v-show="noClickAllowed">{{noClickAllowed}}</p>
      </div>
    </div>
</template>
<script>
export default {
    name: 'appButtons',
    props: {
    isWatchedStopped: Boolean,
    counter: Number,
    timeOutMessage: String,
    noClickAllowed: String
    },
    methods: {
        shuffleCards(){
            this.$emit('shuffleCards')
        },
        startCounter(){
            this.$emit('startCounter')
        },
        clearTimer(){
            this.$emit('clearTimer')
        }
    }
}
</script>
<style scoped>

.counter-shuffle-btn-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 50px;
}
.counter {
  margin-left: 50px;
}
.shuffle-btn,
.stop-timer-btn {
  padding: 5px;
  border-radius: 10px;
  background-color: darkgreen;
  color: white;
  font-weight: bold;
}
</style>