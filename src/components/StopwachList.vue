<template>
  <stopwatch-item v-for="stopwach in stopwaches" :key="stopwach.id" v-bind:stopwach="stopwach" />
</template>

<script>
import StopwatchItem from './StopwatchItem.vue';

export default {
  components: {
    StopwatchItem,
  },
  emits: ['changeTime', 'changeIsActive', 'changeTimer'],

  props: {
    stopwaches: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style></style>
