<template>
  <button :disabled="disabled" @click="whack" />
</template>

<script>
export default {
  name: 'Mole',
  emits: ['whacked', 'escaped'],
  data() {
    return {
      timer: null,
    };
  },
  unmounted() {
    clearTimeout(this.timer);
  },
  props: ['disabled'],
  watch: {
    disabled: function(current) {
      if (current === false) {
        this.timer = setTimeout(() => {
          this.$emit('escaped');
        }, 500);
      }
    },
  },
  methods: {
    whack: function() {
      this.$emit('whacked');
      clearTimeout(this.timer);
    },
  },
};
</script>

<style scoped>
button {
  width: 64px;
  height: 64px;
  border-style: solid;
  border-radius: 999px;
  color: white;
  background-color: green;
}

button:disabled {
  background-color: grey;
}
</style>
