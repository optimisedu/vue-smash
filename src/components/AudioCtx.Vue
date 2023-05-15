  <script>
  export default {
    name: 'AudioCtx',
    data() {
      return {
        audioContext: null,
      };
    },
    mounted() {
      this.audioContext = new (window.AudioContext || window.webkitAudioContext)();
    },
    methods: {
      SmashSound() {
        let oscillator = this.audioContext.createOscillator();
        let filter = this.audioContext.createBiquadFilter();
  
        oscillator.type = 'sine';
        oscillator.frequency.setValueAtTime(400, this.audioContext.currentTime);
        filter.frequency.setValueAtTime(1000, this.audioContext.currentTime);
  
        oscillator.connect(filter);
        filter.connect(this.audioContext.destination);
  
        oscillator.start();
        oscillator.stop(this.audioContext.currentTime + 0.3);
      },
      gameOver() {
        let oscillator = this.audioContext.createOscillator();
        let filter = this.audioContext.createBiquadFilter();
  
        oscillator.type = 'triangle';
        oscillator.frequency.setValueAtTime(100, this.audioContext.currentTime);
        filter.frequency.setValueAtTime(200, this.audioContext.currentTime);
  
        oscillator.connect(filter);
        filter.connect(this.audioContext.destination);
  
        oscillator.start();
        oscillator.stop(this.audioContext.currentTime + 1);
      },
    },
  };
  </script>
  