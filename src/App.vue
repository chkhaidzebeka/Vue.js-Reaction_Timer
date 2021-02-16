<template>
  <h1>Reaction Timer</h1>
  <input 
    type="number"
    v-model="elements"
    :readonly="isPlaying"
    placeholder="How many elements do you want?"
  >
  <button @click="start" :disabled="isPlaying">Play</button>
  <p>We will generate {{ elements }} elements.</p>
  <hr>
  <p v-show="started">Please wait... Be prepared :)</p>
  <Block 
    v-if="isPlaying" 
    :delay="delay" 
    :index="index" 
    :elements="parseInt(elements)"
    @end="endGame"
    @started="this.started=false"
  />
  <Result v-if="showResult" :score="score" />
</template>

<script>
import Block from './components/Block.vue';
import Result from './components/Results.vue'

export default {
  name: 'App',
  components: {Block, Result},
  data() {
    return {
      isPlaying: false,
      showResult: false,
      started: false,
      delay: null,
      score: null,
      elements: 10
    }
  },
  methods: {
    random(min,max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    },
    start() {
      this.delay = this.random(2,7);
      this.index = this.random(1,this.delay-1);
      this.isPlaying = true;
      this.showResult = false;
      this.started = true;
    },
    endGame(reactionTime,showResult) {
      this.score = reactionTime;
      this.isPlaying = false;
      this.showResult = showResult;
    }
  }
}
</script>

<style>
body {
  max-width: 1040px;
  margin: 0 auto;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

button {
  padding: 10px 20px;
  border: none;
  border-radius: 2px;
  background: cornflowerblue;
  width: 100px;
  color: #fff;
  cursor: pointer;
}

button:hover {
  transform: scale(1.02);
}

button:active,
button:focus {
  outline: none;
}

button:disabled {
  background: darkgray;
  cursor: not-allowed;
}

input {
  outline: none;
  border: 2px solid #126c44;
  padding: 8px;
  margin-right: 10px;
}
</style>
