<template>
  <h1>Reaction Timer</h1>
  <code>Score = ReactionTime * Number of elements</code>
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
  <Result 
    v-if="showResult" 
    :elements="parseInt(elements)" 
    :reactionTime="reactionTime"
  />
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
      reactionTime: null,
      elements: 10
    }
  },
  methods: {
    random(min,max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    },
    start() {
      this.delay = this.random(2,7);
      this.index = this.random(1,this.elements);
      this.isPlaying = true;
      this.showResult = false;
      this.started = true;
    },
    endGame(reactionTime,showResult) {
      this.reactionTime = reactionTime;
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
  width: 70%;
  margin: 0 auto;
}

button {
  padding: 10px 20px;
  border: none;
  border-radius: 2px;
  background: cornflowerblue;
  width: 100px;
  color: #fff;
  cursor: pointer;
  margin-top: 10px;
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
  width: 230px;
  border: 2px solid #126c44;
  padding: 8px;
  margin-right: 10px;
}

code {
  display: block;
  border: 1px solid #1d2c67;
  padding: 5px;
  max-width: 350px;
  background: #e4e0ff;
  margin: 0 auto 10px auto;
}
</style>
