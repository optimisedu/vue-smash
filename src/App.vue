<template>
  <div>
    <h1>Smash a Light!</h1>
    <score-input @update="updateDesiredScore" />
    <div class="lights">
      <light
        v-for="light in lights"
        :key="light.id"
        :is-on="light.isOn"
        @smashed="handleSmashed(light)"
      />
    </div>
    <button @click="turnOnRandomLight">
      Smash a Light!
    </button>
    <div class="score">
      <span>Score: {{ score }}</span>
    </div>
    <div v-if="isGameOver">
      <span>Game Over!</span>
    </div>
  </div>
</template>

<script>
import Light from './components/Light.vue';
import ScoreInput from './components/ScoreInput.vue';

export default  {
  name: 'App',
  components: {
    Light,
    ScoreInput,
  },
  data() {
    return {
      lights: [
        {
          id: 'light-1',
          isOn: false,
        },
        {
          id: 'light-2',
          isOn: false,
        },
        {
          id: 'light-3',
          isOn: false,
        },
        {
          id: 'light-4',
          isOn: false,
        },
        {
          id: 'light-5',
          isOn: false,
        },
      ],

      score: 0,
      desiredScore: 0, // Reintroduced desiredScore
    };
  },
  computed: {
    isGameOver() {
      // Game is over if score reaches desiredScore
      return this.score >= this.desiredScore;
    },
  },
  methods: {
    updateDesiredScore(newScore) {
      this.desiredScore = newScore;
    },
    turnOnRandomLight() {
      const randomIndex = Math.floor(Math.random() * this.lights.length);
      const light = this.lights[randomIndex];
      console.log(`Turning on light ${light.id}`);
      light.isOn = true;
    },
    handleSmashed(light) {
      if (light.isOn) {
        light.isOn = false;
        this.score += 1;

        if (!this.isGameOver) {
          this.turnOnRandomLight();
        } else {
          alert('Game Over!');
        }
      }
    },
  },
};
</script>
<style>
.lights {
  display: flex;
  flex-wrap: wrap;
}

.light {
  width: 100px;
  height: 100px;
  background-color: lightgray;
  border-radius: 50%;
  margin: 10px;
  cursor: pointer;
}

.light.is-on {
  background-color: red;
}
</style>