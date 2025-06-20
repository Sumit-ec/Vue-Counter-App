<!-- <template>
  <div class="timer-unit">
    <h3>Timer {{ id }}</h3>
    <div class="timer">{{ count }}</div>
    <CountdownControl
      :isRunning="interval !== null"
      @start="start"
      @stop="stop"
    />
    <button @click="emitRemove">Remove</button>
  </div>
</template>

<script>
import CountdownControl from "./CountdownControl.vue";

export default {
  name: "TimerUnit",
  components: {
    CountdownControl,
  },
  props: {
    id: Number,
  },
  data() {
    return {
      count: 0,
      interval: null,
    };
  },
  methods: {
    start() {
      if (this.interval) return;
      this.interval = setInterval(() => {
        this.count++;
      }, 1000);
    },
    stop() {
      clearInterval(this.interval);
      this.interval = null;
    },
    emitRemove() {
      this.stop();
      this.$emit("remove", this.id);
    },
  },
};
</script>


<style>
.timer-unit {
  border: 1px solid black;
  padding: 10px;
  border-radius: 4px;
  box-shadow: 5px 5px deepskyblue;
}
</style> -->



<template>
  <div class="timer-unit">
    <h3>Timer {{ id }}</h3>
    <div class="timer">{{ count }}</div>
    <CountdownControl
      :isRunning="interval !== null"
      @start="start"
      @stop="stop"
    />
    <button @click="emitRemove">Remove</button>
  </div>
</template>

<script>
import CountdownControl from "./CountdownControl.vue";

export default {
  name: "TimerUnit",
  components: {
    CountdownControl,
  },
  props: {
    id: Number,
  },
  data() {
    return {
      count: 0,
      interval: null,
    };
  },
  methods: {
    start() {
      if (this.interval) return;
      this.interval = setInterval(() => {
        this.count++;
      }, 1000);
      this.$emit("status", { id: this.id, isRunning: true });
    },
    stop() {
      clearInterval(this.interval);
      this.interval = null;
      this.$emit("status", { id: this.id, isRunning: false });
    },
    emitRemove() {
      this.stop();
      this.$emit("remove", this.id);
    },
  },
  beforeDestroy() {
    this.stop();
  },
};
</script>

<style scoped>
.timer-unit {
  border: 2px solid #42b983;
  border-radius: 10px;
  padding: 20px;
  width: 120px;
  box-shadow: 2px 2px 0 #3498db;
}
.timer {
  font-size: 2rem;
  margin: 10px 0;
  font-weight: bold;
}
button {
  padding: 5px 10px;
  margin: 5px 0;
}
</style>
