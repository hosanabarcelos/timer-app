<template>
  <div id="app" v-cloak>
    <img src="../public/images/illustration.svg" />
    <timer-setup v-if="!time" @set-time="setTime"></timer-setup>
    <div v-else style="margin-left: 58px">
      <timer :time="time"></timer>
      <div>
        <button v-if="!isRunning" @click="start">Iniciar</button>
        <button v-if="isRunning" @click="stop">Pausar</button>
        <button @click="reset">Reiniciar</button>
      </div>
    </div>
  </div>
</template>



  <script>
import TimerSetup from "./timer-setup.vue";
import Timer from "./timer.vue";
import icon from "@/public/images/clock.svg";

export default {
  data() {
    return {
      isRunning: false,
      hours: 0,
      minutes: 0,
      seconds: 0,
      time: 0,
      timer: null,
      sound: null,
    };
  },
  computed: {
    prettyTime() {
      let time = this.time;
      let hours = Math.floor(time / 3600);
      time %= 3600;
      let minutes = Math.floor(time / 60);
      let seconds = time % 60;
      return hours + ":" + minutes + ":" + seconds;
    },
  },
  methods: {
    start() {
      this.isRunning = true;
      if (!this.timer) {
        this.timer = setInterval(() => {
          if (this.time > 0) {
            this.time--;
          } else {
            clearInterval(this.timer);
            this.notify();
            this.reset();
          }
        }, 1000);
      }
    },
    stop() {
      this.isRunning = false;
      clearInterval(this.timer);
      this.timer = null;
    },
    reset() {
      this.stop();
      this.time = 0;
      this.seconds = 0;
      this.minutes = 0;
      this.hours = 0;
    },
    setTime(payload) {
      this.time = payload.hours * 3600 + payload.minutes * 60 + payload.seconds;
    },
    notify() {
      this.sound.play().catch((error) => console.log(error));
      if (Notification.permission === "granted") {
        new Notification("00:00:00", {
          body: "O tempo acabou!",
          icon: icon,
        });
      } else if (Notification.permission !== "denied") {
        Notification.requestPermission().then((permission) => {
          if (permission === "granted") {
            new Notification("00:00:00", {
              body: "O tempo acabou!",
              icon: icon,
            });
          }
        });
      }
    },
  },
  components: {
    TimerSetup,
    Timer,
  },
  mounted() {
    this.sound = new Audio("../public/audios/computer-space.mp3");
  },
};
</script>

<style scoped>
#app {
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

img {
  width: 24rem;
}

body {
  font-family: sans-serif;
  padding: 0;
  margin: 0;
}

input[type="number"] {
  padding: 10px;
  font-size: inherit;
  width: 100%;
}

[v-cloak] {
  opacity: 0;
}

label {
  width: 20%;
  padding: 10px 0;
  display: inline-block;
}

.timer {
  font-size: 2em;
  margin: 20px;
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
  padding: 10px 32px;
  text-align: center;
  transition: color 100ms;
  margin-right: 8px;
}

button:hover {
  background-color: #4791df;
}
</style>
