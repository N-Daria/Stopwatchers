<template>
  <main class="body">
    <ul class="stopwachList">
      <stopwach-list
        v-bind:stopwaches="stopwaches"
        @changeTime="changeTime"
        @changeIsActive="changeIsActive"
        @changeTimer="changeTimer"
      />

      <button class="stopwachList__new-stopwach stopwachList__block" @click="createTimer"></button>
    </ul>
  </main>
</template>

<script>
import StopwachList from './StopwachList.vue';

export default {
  components: {
    StopwachList,
  },

  data() {
    return {
      stopwaches: [
        {
          time: 0,
          id: Date.now(),
          isActive: false,
          timer: null,
        },
      ],
    };
  },

  methods: {
    createTimer() {
      const newStopwach = {
        time: 0,
        id: Date.now(),
        isActive: false,
        timer: null,
      };
      this.stopwaches.push(newStopwach);
    },

    findStopwach(id) {
      return this.stopwaches.filter((el) => el.id === id)[0];
    },

    changeTime(value, id) {
      const stopwach = this.findStopwach(id);
      stopwach.time = value;
    },

    changeIsActive(value, id) {
      const stopwach = this.findStopwach(id);
      stopwach.isActive = value;
    },

    changeTimer(value, id) {
      const stopwach = this.findStopwach(id);
      stopwach.timer = value;
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

.stopwachList__block {
  min-height: 120px;
  background-color: #696969;
}

.stopwachList__new-stopwach {
  background-image: url(../assets/icons/add.svg);
  background-position: center;
  background-repeat: no-repeat;
  background-size: 20px;
  background-color: #696969;
}
</style>
