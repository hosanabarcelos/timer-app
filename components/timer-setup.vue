<template>
  <form :class="{ 'timer-form': true, 'timer-set': isTimeSet }">
    <label for="hrs" class="time-part">
      <input
        type="number"
        v-model="hours"
        name="time_h"
        id="hrs"
        min="0"
        max="23"
      />
      <span class="time-label">h</span>
    </label>
    <label for="min" class="time-part">
      <input
        type="number"
        v-model="minutes"
        name="time_m"
        id="min"
        min="0"
        max="59"
      />
      <span class="time-label">m</span>
    </label>
    <label for="sec" class="time-part">
      <input
        type="number"
        v-model="seconds"
        name="time_s"
        id="sec"
        max="59"
        min="0"
      />
      <span class="time-label">s</span>
    </label>
    <div>
        <button type="button" @click="sendTime">Ok</button>
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
  methods: {
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
  color: #767676;
}

.timer-form input {
  font-size: 2em;
  padding: 0;
  border: none;
  border-bottom: 2px solid #767676;
  background: transparent;
  width: 100px;
  text-align: center;
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
  color: #767676;
  border: 0;
}

.timer-form .time-part input:focus {
  border: 0 !important;
}

button {
  background-color: #6A40BF;
  border-radius: 8px;
  border-style: none;
  color: #FFFFFF;
  cursor: pointer;
  font-size: 14px;
  font-weight: 500;
  height: 40px;
  line-height: 20px;
  margin: 0;
  outline: none;
  padding: 10px 16px;
  text-align: center;
  transition: color 100ms;
  margin-right: 8px;
}

button:hover {
  background-color: #805ec2;
}

</style>



