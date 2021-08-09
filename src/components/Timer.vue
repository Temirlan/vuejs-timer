<template>
  <div>
    <h1>{{ name }}</h1>
    <div class="timer">{{ prettyTime() }}</div>
    <p v-if="startTime">Start time: {{ startTime }}</p>
    <p v-if="finishTime">Finish time: {{ finishTime }}</p>
    <hr align="center" size="2" color="#0000dd" />
  </div>
</template>

<script>
export default {
  name: 'Timer',
  props: {
    time: {},
    name: String,
  },
  data: function() {
    return {
      isRunning: false,
      timer: null,
      t: this.time,
      finishTime: null,
      startTime: null,
    };
  },
  mounted() {
    this.start();
  },
  methods: {
    start() {
      this.startHandler();
      this.isRunning = true;

      if (!this.timer) {
        this.timer = setInterval(() => {
          if (this.t > 0) {
            this.t = this.t - 10;
          } else {
            clearInterval(this.timer);
            this.reset();
          }
        }, 10);
      }
    },
    stop() {
      this.isRunning = false;
      clearInterval(this.timer);
      this.timer = null;
    },
    reset() {
      this.stop();
      this.t = 0;
      this.finishHandler();
    },

    getNowFormattedTime() {
      const d = new Date();

      let dateByFormat =
        ('0' + d.getHours()).slice(-2) +
        ':' +
        ('0' + d.getMinutes()).slice(-2) +
        ':' +
        ('0' + d.getSeconds()).slice(-2);

      return dateByFormat;
    },

    finishHandler() {
      this.finishTime = this.getNowFormattedTime();
    },

    startHandler() {
      this.startTime = this.getNowFormattedTime();
    },

    prettyTime() {
      let time = this.t / 1000;
      let secondes = parseInt(time);
      let milliseconds = Math.round((time - secondes) * 1000);

      if (secondes < 10) {
        secondes = '0' + secondes;
      }

      if (milliseconds < 10) {
        milliseconds = '00' + milliseconds;
      }

      if (milliseconds > 10 && milliseconds < 100) {
        milliseconds = '0' + milliseconds;
      }

      return secondes + ':' + milliseconds;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
