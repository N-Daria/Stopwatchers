<template>
  <stopwatch-item
    v-for="stopwach in stopwaches"
    :key="stopwach.id"
    v-bind:stopwach="stopwach"
    @passTime="passTime"
    @passIsActive="passIsActive"
    @passTimer="passTimer"
  />
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
  methods: {
    passTime(value, id) {
      this.$emit('changeTime', value, id);
    },

    passIsActive(value, id) {
      this.$emit('changeIsActive', value, id);
    },

    passTimer(value, id) {
      this.$emit('changeTimer', value, id);
    },
  },
};
</script>

<style></style>
