<template>
  <div class="controls">
    <button @click="toggle">
      {{ isRunning ? "Stop" : "Start" }}
    </button>
  </div>
</template>

<script>
export default {
  name: "CountdownControl",
  props: {
    isRunning: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    toggle() {
      this.$emit(this.isRunning ? "stop" : "start");
    },
  },
};
</script>

<style scoped>
.controls button {
  font-size: 1.2rem;
  padding: 10px 20px;
  margin: 10px 0;
  cursor: pointer;
}
</style>
