<template>
  <form>
    <label for="min"
      >Secondes<br />
      <input
        :value="secondes"
        @input="secondesChangeHandler"
        type="number"
        name="time_m"
        id="sec"
        min="0"
        max="59"
      />
    </label>
    <label for="sec"
      >Milliseconds<br />
      <input
        :value="milliseconds"
        @input="millisecondsChangeHandler"
        type="number"
        name="time_s"
        id="mil"
        max="999"
        min="0"
      />
    </label>
    <button type="button" @click="clickHandler">Start</button>
  </form>
</template>

<script>
export default {
  name: 'CreateTimerForm',
  props: {
    msg: String,
  },
  data() {
    return {
      secondes: 0,
      milliseconds: 0,
    };
  },
  methods: {
    secondesChangeHandler(event) {
      const value = event.target.value;

      if (String(value).length <= 2 && String(value) < 60) {
        this.secondes = value;
      }

      this.$forceUpdate();
    },

    millisecondsChangeHandler(event) {
      const value = event.target.value;

      if (String(value).length <= 3 && String(value) < 1000) {
        this.milliseconds = value;
      }

      this.$forceUpdate();
    },

    clickHandler() {
      this.$emit('add-timer', {
        secondes: this.secondes,
        milliseconds: this.milliseconds,
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
