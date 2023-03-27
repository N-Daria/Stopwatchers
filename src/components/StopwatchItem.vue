<template>
  <li class="stopwach stopwachList__block">
    <p class="stopwach__time" v-bind:class="{ stopwach__time_stopped: !stopwach.isActive }">
      {{ formattedTime }}
    </p>
    <button
      v-if="!stopwach.isActive"
      class="stopwach__button stopwach__button_start"
      v-bind:class="{ stopwach__button_stopped: !stopwach.isActive }"
      @click="setTimer"
    ></button>
    <button
      v-if="stopwach.isActive"
      class="stopwach__button stopwach__button_stop"
      v-bind:class="{ stopwach__button_stopped: !stopwach.isActive }"
      @click="stopTimer"
    ></button>
    <button
      class="stopwach__button stopwach__button_reset"
      v-bind:class="{ stopwach__button_stopped: !stopwach.isActive }"
      @click="resetTimer"
    ></button>
  </li>
</template>

<script>
export default {
  props: {
    stopwach: {
      type: Object,
      required: true,
    },
  },

  methods: {
    setTimer() {
      this.stopwach.isActive = true;

      this.stopwach.timer = setInterval(() => {
        this.stopwach.time += 1;
      }, 1000);
    },

    resetTimer() {
      this.stopwach.time = 0;
    },

    stopTimer() {
      this.stopwach.isActive = false;
      clearInterval(this.stopwach.timer);
    },
  },

  computed: {
    formattedTime() {
      let newTime = this.stopwach.time;

      if (newTime > 60) {
        const date = new Date(1990, 1, 1, 0, 0, this.stopwach.time);

        if (date.getMinutes() > 0) {
          newTime = `${date.getMinutes()}:${date.getSeconds()}`;
        }
        if (date.getHours() > 0) {
          newTime = `${date.getHours()}:${date.getMinutes()}:${date.getSeconds()}`;
        }
      }

      return newTime;
    },
  },
};
</script>

<style>
.stopwach {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  color: white;
}

.stopwach__time {
  border-bottom: 1px white solid;
  padding: 19px 0;
  color: inherit;
  font-family: 'Gotham Pro', 'Arial', 'sans-serif';
  font-style: normal;
  font-weight: 400;
  font-size: 22px;
  line-height: 21px;
  text-align: center;
  width: 100%;
  margin: 0;
}

.stopwach__time_stopped,
.stopwach__button_stopped {
  opacity: 0.3;
}

.stopwach__button {
  background-position: center;
  background-repeat: no-repeat;
  background-size: 20px;
  background-color: inherit;
  width: 20px;
  height: 20px;
  margin: 20px 0;
}

.stopwach__button_start {
  background-image: url(../assets/icons/треугольник.svg);
}

.stopwach__button_stop {
  background-image: url(../assets/icons/Пауза.svg);
}

.stopwach__button_reset {
  background-image: url(../assets/icons/квадрат.svg);
}
</style>
