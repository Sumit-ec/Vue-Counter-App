<template>
  <div id="app">
    <h1>Multiple Countdown Timers</h1>
    <div class="buttons">
      <button @click="addTimer">Add Timer</button>
      <button @click="toggleAll">
        {{ allRunning ? " Stop All" : " Start All" }}
      </button>
    </div>

    <div class="timers">
      <TimerUnit
        v-for="id in timers"
        :key="id"
        :id="id"
        ref="timerRefs"
        @remove="removeTimer(id)"
        @status="updateTimerState"
      />
    </div>
  </div>
</template>

<script>
import TimerUnit from "./components/TimerUnit.vue";

export default {
  name: "App",
  components: { TimerUnit },
  data() {
    return {
      timers: [],
      timerStates: {}, // to track isRunning status
      nextId: 1,
    };
  },
  computed: {
    allRunning() {
      const values = Object.values(this.timerStates);
      return values.length > 0 && values.every(Boolean);
    },
  },
  methods: {
    addTimer() {
      const id = this.nextId++;
      this.timers.push(id);
      this.$set(this.timerStates, id, false);
    },
    removeTimer(id) {
      this.timers = this.timers.filter((t) => t !== id);
      this.$delete(this.timerStates, id);
    },
    toggleAll() {
      const shouldStart = !this.allRunning;
      const timerList = this.$refs.timerRefs;

      this.timers.forEach((id) => {
        const comp = Array.isArray(timerList)
          ? timerList.find((c) => c.id === id)
          : timerList[id];
        if (comp) {
          shouldStart ? comp.start() : comp.stop();
        }
      });
    },
    updateTimerState({ id, isRunning }) {
      this.$set(this.timerStates, id, isRunning);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 30px;
}
.buttons {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 20px;
}
.timers {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 15px;
}
</style>
