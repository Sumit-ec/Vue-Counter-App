<template>
  <div class="timer">
    <h2>{{ count }}</h2>
  </div>
</template>

<script>
export default {
  name: "CountdownTimer",
  props: {
    count: {
      type: Number,
      required: true,
    },
  },
};
</script>

<style scoped>
.timer {
  font-size: 3rem;
  margin: 20px 0;
}
</style>
