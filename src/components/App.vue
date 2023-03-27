<template>
  <main class="body">
    <ul class="stopwachList">
      <!-- <stopwachList v-bind:stopwaches="stopwaches" /> -->

      <!-- <li class="stopwach stopwachList__block" v-for="item in stopwaches" :key="item.id">


      </li> -->

      <li class="stopwach stopwachList__block">
        <p
          class="stopwach__time"
          v-bind:class="{ stopwach__time_stopped: !this.stopwach.isActive }"
        >
          {{ formattedTime }}
        </p>
        <button
          v-if="!stopwach.isActive"
          class="stopwach__button stopwach__button_start"
          v-bind:class="{ stopwach__button_stopped: !this.stopwach.isActive }"
          @click="setTimer"
        ></button>
        <button
          v-if="stopwach.isActive"
          class="stopwach__button stopwach__button_stop"
          v-bind:class="{ stopwach__button_stopped: !this.stopwach.isActive }"
          @click="stopTimer"
        ></button>
        <button
          class="stopwach__button stopwach__button_reset"
          v-bind:class="{ stopwach__button_stopped: !this.stopwach.isActive }"
          @click="resetTimer"
        ></button>
      </li>

      <button class="stopwachList__new-stopwach stopwachList__block" @click="createTimer"></button>
    </ul>
  </main>
</template>

<script>
// import stopwachList from './stopwachList.vue';

export default {
  // components: {
  //   stopwachList,
  // },

  data() {
    return {
      stopwach: {
        time: 0,
        id: Date.now(),
        isActive: false,
        timer: null,
      },

      // stopwaches: [
      //   {
      //     time: 0,
      //     id: Date.now(),
      //     isSet: true,
      //   },
      //   {
      //     time: '25:32',
      //     id: Date.now(),
      //     isSet: true,
      //   },
      //   {
      //     time: '1:30:15',
      //     id: Date.now(),
      //     isSet: true,
      //   },
      // ],
    };
  },

  methods: {
    createTimer() {
      const newStopwach = {
        time: 4,
        id: Date.now(),
        isSet: false,
      };
      this.stopwaches.push(newStopwach);
    },

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
button {
  border: none;
  cursor: pointer;
}

#app {
  background-color: #353638;
  max-width: 776px;
  min-width: 320px;
  margin: 0 auto;
}

.body {
  min-height: 100vh;
  align-items: center;
  display: flex;
  padding: 130px 0;
  box-sizing: border-box;
}

@media (max-width: 1200px) {
  .body {
    padding: 72px 0 82px;
  }
}

@media (max-width: 768px) {
  .body {
    padding: 72px 0 72px;
  }
}

.stopwachList {
  display: grid;
  grid-template-columns: repeat(auto-fill, 225px);
  gap: 45px 50px;
  list-style-type: none;
  margin: 0 auto;
  width: 100%;
  padding: 0;
}

.stopwachList__block {
  min-height: 120px;
  background-color: #696969;
}

@media (max-width: 1199px) {
  .stopwachList {
    max-width: 500px;
  }
}

@media (max-width: 767px) {
  .stopwachList {
    max-width: 225px;
  }
}

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

.stopwachList__new-stopwach {
  background-image: url(../assets/icons/add.svg);
  background-position: center;
  background-repeat: no-repeat;
  background-size: 20px;
  background-color: #696969;
}
</style>
