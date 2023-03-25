<template>
  <main class="body">
    <ul class="stopwachList">
      <li class="stopwach stopwachList__block" v-for="item in stopwaches" :key="item.id">
        <p class="stopwach__time">{{ item.stopwach }}</p>
        <button class="stopwach__button stopwach__button_start" @click="setTimer"></button>
        <button class="stopwach__button stopwach__button_stop" @click="stopTimer"></button>
        <button class="stopwach__button stopwach__button_reset" @click="resetTimer"></button>
      </li>

      <button class="stopwachList__new-stopwach stopwachList__block" @click="createTimer"></button>
    </ul>
  </main>
</template>

<script>
export default {
  data() {
    return {
      stopwaches: [
        { stopwach: '2:40', id: 1, isSet: false },
        { stopwach: '25:32', id: 2, isSet: false },
        { stopwach: '1:30:15', id: 3, isSet: false },
      ],
    };
  },
  methods: {
    setTimer() {},
    resetTimer() {},
    stopTimer() {},

    createTimer() {
      const newStopwach = {
        timer: 4,
        id: 4,
        isSet: false,
      };
      this.stopwaches.push(newStopwach);
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
