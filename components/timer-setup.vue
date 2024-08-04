<template>
  <form :class="{ 'timer-form': true, 'timer-set': isTimeSet }">
    <div class="timer-form-container">
      <div class="timer-form-content">
        <label for="hrs" class="time-part">
          <input
            type="number"
            v-model="formattedHours"
            name="time_h"
            id="hrs"
            min="0"
            max="23"
            @input="updateHours"
          />
          <span class="time-label">h</span>
        </label>
        <label for="min" class="time-part">
          <input
            type="number"
            v-model="formattedMinutes"
            name="time_m"
            id="min"
            min="0"
            max="59"
            @input="updateMinutes"
          />
          <span class="time-label">m</span>
        </label>
        <label for="sec" class="time-part">
          <input
            type="number"
            v-model="formattedSeconds"
            name="time_s"
            id="sec"
            max="59"
            min="0"
            @input="updateSeconds"
          />
          <span class="time-label">s</span>
        </label>
      </div>
      <div>
        <button type="button" @click="sendTime">Ok</button>
      </div>
    </div>
  </form>
</template>




<script>
export default {
  data() {
    return {
      hours: 0,
      minutes: 0,
      seconds: 0,
      isTimeSet: false,
    };
  },
  computed: {
    formattedHours() {
      return this.hours < 10 ? "0" + this.hours : this.hours.toString();
    },
    formattedMinutes() {
      return this.minutes < 10 ? "0" + this.minutes : this.minutes.toString();
    },
    formattedSeconds() {
      return this.seconds < 10 ? "0" + this.seconds : this.seconds.toString();
    },
  },
  methods: {
    updateHours(event) {
      let value = parseInt(event.target.value, 10);
      if (isNaN(value) || value < 0 || value > 23) {
        value = 0;
      }
      this.hours = value;
    },
    updateMinutes(event) {
      let value = parseInt(event.target.value, 10);
      if (isNaN(value) || value < 0 || value > 59) {
        value = 0;
      }
      this.minutes = value;
    },
    updateSeconds(event) {
      let value = parseInt(event.target.value, 10);
      if (isNaN(value) || value < 0 || value > 59) {
        value = 0;
      }
      this.seconds = value;
    },
    sendTime() {
      this.isTimeSet = true;
      this.$emit("set-time", {
        hours: this.hours,
        minutes: this.minutes,
        seconds: this.seconds,
      });
    },
  },
};
</script>


<style scoped>
.timer-form {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 2em;
  color: #ffffff;
  margin-left: 68px;
}

.timer-form-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 14px;
}

.timer-form-content {
  display: flex;
  align-items: center;
  gap: 14px;
}

.timer-form input {
  font-size: 2em;
  padding: 0;
  border: none;
  background: transparent;
  width: 100px;
  text-align: center;
}

input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

.timer-form input:focus {
  outline: none;
  box-shadow: none;
}

.timer-form .time-label {
  font-size: 0.5em;
  vertical-align: super;
  margin-left: 2px;
}

.timer-form .time-part {
  margin: 0 5px;
  display: flex;
  align-items: center;
}

.timer-form .time-part input {
  font-size: 4rem;
  color: #ffffff;
  border: 0;
}

.timer-form .time-part input:focus {
  border: 0 !important;
}

button {
  background-color: #3178c6;
  border-radius: 8px;
  border-style: none;
  color: #ffffff;
  cursor: pointer;
  font-size: 16px;
  font-weight: 500;
  height: 40px;
  line-height: 20px;
  margin: 0;
  outline: none;
  padding: 10px 54px;
  text-align: center;
  transition: color 100ms;
  margin-right: 8px;
}

button:hover {
  background-color: #4791df;
}
</style>



