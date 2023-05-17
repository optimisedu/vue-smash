<template>
  <div @click="handleClick">
    <svg
      :class="{'light-on': isOn}"
      class="light"
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      stroke-width="2"
      stroke-linecap="round"
      stroke-linejoin="round"
    >
      <circle cx="12" cy="12" r="10" />
    </svg>
  </div>
</template>

<script>
export default {
  name: 'Light',
  props: ['isOn'],
  methods: {
    handleClick() {
      this.$emit('smashed');
    },
  },
};
</script>

<style scoped>
.light {
  width: 100px;
  height: 100px;
  stroke: lightgray;
  cursor: pointer;
  transition: stroke 0.3s;
}

.light.light-on {
  animation: pulse 1s infinite;
  stroke: red;
}

@keyframes pulse {
  0% {
    transform: scale(0.95);
  }

  70% {
    transform: scale(1);
  }

  100% {
    transform: scale(0.95);
  }
}
</style>
