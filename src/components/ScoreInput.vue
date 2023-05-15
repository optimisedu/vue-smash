<!-- ScoreInput.vue -->
<template>
    <div>
      <label for="desired-score">Desired Score:</label>
      <input
        id="desired-score"
        type="number"
        v-model="desiredScore"
        @input="emitDesiredScore"
      />
    </div>
  </template>
  
  <script>
  export default {
    name: 'ScoreInput',
    data() {
      return {
        desiredScore: 0,
      };
    },
    methods: {
      emitDesiredScore() {
        this.$emit('update', this.desiredScore);
      },
    },
  };
  </script>
  