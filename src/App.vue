<template>
  <div>
    <h1>Smash a Light!</h1>
    <score-input @update="updateDesiredScore" />
    <select v-model="difficulty" @change="changeDifficulty">
      <option value="easy">Easy</option>
      <option value="medium">Medium</option>
      <option value="hard">Hard</option>
    </select>
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
      difficulty: 'easy',
      speed: 2000,
      lights: Array(5).fill().map((_, i) => ({ id: `light-${i + 1}`, isOn: false })),
      score: 0,
      desiredScore: 0,
    };
  },
  computed: {
    isGameOver() {
      return this.score >= this.desiredScore;
    },
  },
  methods: {
    updateDesiredScore(newScore) {
      this.desiredScore = newScore;
    },
    turnOnRandomLight() {
      console.log('turnOnRandomLight called');
      if (this.isGameOver) {
        this.resetGame();
      } else {
        this.lights.forEach(light => light.isOn = false);
        const randomIndex = Math.floor(Math.random() * this.lights.length);
        const light = this.lights[randomIndex];
        console.log(`Turning on light ${light.id}`);
        light.isOn = true;

        setTimeout(() => {
          light.isOn = false;
        }, this.speed);
      }
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
    //move to settings
    changeDifficulty() {
      switch (this.difficulty) {
        case 'easy':
          this.lights = Array(5).fill().map((_, i) => ({ id: `light-${i + 1}`, isOn: false }));
          this.speed = 2000;
          break;
        case 'medium':
          this.lights = Array(10).fill().map((_, i) => ({ id: `light-${i + 1}`, isOn: false }));
          this.speed = 1500;
          break;
        case 'hard':
          this.lights = Array(15).fill().map((_, i) => ({ id: `light-${i + 1}`, isOn: false }));
          this.speed = 1000;
          break;
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
