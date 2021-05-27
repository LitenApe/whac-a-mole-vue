<template>
  <h2>Whac-a-Mole</h2>
  <p>Points: {{ points * 10 }}</p>

  <button v-if="progress === -1" @click="resetRound">Start</button>

  <div>
    <Mole v-for="n in 9" :key="n" :disabled="active !== n" @escaped="escaped" @whacked="whacked" />
  </div>
</template>

<script>
import Mole from './Mole';

export default {
  name: 'Game',
  components: { Mole },
  data() {
    return {
      progress: -1,
      points: 0,
      timer: null,
      active: -1,
    };
  },
  emits: ['save'],
  unmounted() {
    clearTimeout(this.timer);
  },
  computed: {
    score: function() {
      return this.points * 10;
    },
  },
  watch: {
    progress: function(current) {
      if (current === 20) {
        this.$emit('save', this.score);
        clearTimeout(this.timer);
        this.active = -1;
      }
    },
  },
  methods: {
    createTimer: function() {
      this.timer = setTimeout(() => {
        this.active = this.getRandomInt(1, 10);
      }, 3000 - this.progress * 200);
    },
    getRandomInt: function(min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min) + min);
    },
    resetRound: function() {
      this.active = -1;
      this.progress += 1;
      this.createTimer();
    },
    escaped: function() {
      this.resetRound();
    },
    whacked: function() {
      this.points += 1;
      this.resetRound();
    },
  },
};
</script>

<style scoped>
div {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  width: 192px;
  margin: auto;
}
</style>
