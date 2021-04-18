<template>
  <h1>Fastest Finger</h1>
  <button @click="start" :disabled="isPlaying">Play</button>
  <Block v-if="isPlaying" :delay="delay" @end="endGame" />
  <Results v-if="showResults" :score="score" />
  <div class="instruction" v-if="!isPlaying">
    <h4>How to play</h4>
    <ul>
      <li>Click on the 'Play' button to start</li>
      <li>Wait for the 'Click me' box to show</li>
      <li>Click the box as fast as you can, immediately it appears</li>
      <li>
        There are 3 results: 'Fastest finger', 'Fast Reflex' and 'Snail pace'.
        Get 'Fastest Finger' as result to win the game
      </li>
    </ul>
  </div>
</template>

<script>
import Block from "./components/Block.vue";
import Results from "./components/Results";

export default {
  name: "App",
  components: {
    Block,
    Results,
  },
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showResults: false,
    };
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000;
      this.isPlaying = true;
      this.showResults = false;
    },
    endGame(reactionTime) {
      (this.score = reactionTime), (this.isPlaying = false);
      this.showResults = true;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}

button {
  background: #0faf87;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}

button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}

.instruction {
  width: 500px;
  text-align: left;
}
</style>
