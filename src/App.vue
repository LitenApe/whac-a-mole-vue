<template>
  <Game @save="save" />
  <Highscore :scores="sortedScores" />
</template>

<script>
import Highscore from './components/highscore/Highscore';
import Game from './components/game/Game';

export default {
  name: 'App',
  data() {
    return {
      scores: [],
    };
  },
  components: {
    Highscore,
    Game,
  },
  computed: {
    sortedScores: function() {
      return [...this.scores].sort((prev, current) => {
        return prev.score > current.score ? -1 : 1;
      });
    },
  },
  methods: {
    save: function(score) {
      this.scores = [
        ...this.scores,
        {
          score,
          date: new Date().toDateString(),
        },
      ];
    },
  },
};
</script>

<style></style>
