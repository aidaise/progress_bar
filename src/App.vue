<template>
  <div class="progress-container">
    <div>
      <label for="percentInput" class="input-label">Введите процент:</label>
      <input type="number" id="percentInput" class="percent" v-model="percent" @input="setProgressCircle">
    </div>

    <svg class="progress-ring" viewBox="0 0 200 200" preserveAspectRatio="none">
      <circle ref="ci" class="progress-ring__circle"
              stroke="white"
              stroke-width="7"
              cx="100" cy="100"
              :r="radius"
              fill="transparent"
      ></circle>
      <text class="progress-text" x="50%" y="50%" dy=".3em" text-anchor="middle" fill="white" font-size="24">{{ progressInNumber }}%</text>
    </svg>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      radius: 57,
      percent: 1,
    }
  },
  computed: {
    circuit() {
      return 2 * Math.PI * this.radius
    },
    progressInNumber() {
      return this.percent * 100
    },
    circle() {
      return this.$refs.ci
    }
  },
  methods: {
    setProgressCircle() {
      this.circle.style.strokeDashoffset = this.circuit - this.percent * this.circuit
    },
    setStylesToCircle() {
      this.circle.style.strokeDasharray = `${this.circuit} ${this.circuit}`;
      this.circle.style.strokeDashoffset = this.circuit - this.percent * this.circuit;
    }
  },
  mounted() {
    this.setStylesToCircle();
  }
}
</script>

