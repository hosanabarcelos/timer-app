<template>
  <div class="timer">
    <span class="time-part">{{ formattedHours }}</span
    ><span class="time-label">h</span>
    <span class="time-part">{{ formattedMinutes }}</span
    ><span class="time-label">m</span>
    <span class="time-part">{{ formattedSeconds }}</span
    ><span class="time-label">s</span>
  </div>
</template>


<script>
export default {
  props: ["time"],
  computed: {
    formattedHours() {
      const hours = Math.floor(this.time / 3600);
      return hours < 10 ? "0" + hours : hours;
    },
    formattedMinutes() {
      const minutes = Math.floor((this.time % 3600) / 60);
      return minutes < 10 ? "0" + minutes : minutes;
    },
    formattedSeconds() {
      const seconds = this.time % 60;
      return seconds < 10 ? "0" + seconds : seconds;
    },
  },
};
</script>


<style scoped>
span {
  font-size: 4rem;
}
.timer {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 2rem;
  color: #ffffff;
}

.time-part {
  margin: 0 5px;
}

.time-label {
  font-size: 0.5em;
  vertical-align: super;
  margin-left: 2px;
}
</style>

