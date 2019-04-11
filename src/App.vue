<template>
  <div id="app">
    <img src="./assets/engiii.png">
        <h1>Timer</h1>
        <TimerSetup v-if="!time" @set-time="setTime"></TimerSetup>
        <div v-else>
            <Timer :time="filteredTime"></Timer>
            <div>
                <button v-if="!isRunning" @click="start">Start</button>
                <button v-if="isRunning" @click="stop">Stop</button>
                <button @click="reset">Reset</button>
            </div>
        </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Timer from './components/Timer.vue';
import TimerSetup from './components/TimerSetup.vue';

@Component({
  components: {
    Timer,
    TimerSetup
  },
})
export default class App extends Vue {
  sounds: any = new Audio('http://soundbible.com/grab.php?id=1296&type=wav');
  isRunning: boolean = false;
  minutes: number = 0;
  seconds: number = 0;
  time: number = 0;
  timer: any = null;

  get filteredTime(): string {
      let time: number = this.time / 60;
      let minutes: number = Math.floor(time);
      let seconds = Math.round((time - minutes) * 60);
      return (minutes + ":" + seconds).toString();
  }

  start(): void {
      this.isRunning = true;
      if (!this.timer) {
          this.timer = setInterval(() => {
              if (this.time > 0) {
                  this.time--;
              } else {
                  this.sounds.play();
                  clearInterval(this.timer);
                  this.reset();
              }
          }, 1000);
      }
  }

  stop(): void {
      this.isRunning = false;
      clearInterval(this.timer);
      this.timer = null;
  }

  reset(): void {
      this.stop();
      this.time = 0;
      this.seconds = 0;
      this.minutes = 0;
  }

  setTime(payload: {minutes: number, seconds: number}): void {
      this.time = payload.minutes * 60 + payload.seconds;
  }
  
}
</script>

<style>
  html {
    box-sizing: border-box;
  }

  /**, *::before, *::after {*/
    /*box-sizing: inherit;*/
  /*}*/

  .app {
    text-align: center;
    position: center;
    padding: 10px;
    margin: 0 auto;
    max-width: 1000px;
  }

  body {
    font-family: sans-serif;
    padding: 0;
    margin: 0;
  }

  body > div {
    text-align: center;
    position: center;
    padding: 10px;
    margin: 0 auto;
    max-width: 1000px;
  }

  input[type=number] {
    padding: 10px;
    font-size: 1em;
    width: 70%;
  }

  button {
    padding: 14px;
    margin-left: 60px;
    font-size: 1em;
    background: #000;
    color: #fff;
    border: 1px solid #000;
    transition: all 0.3s;
    cursor: pointer;
  }

  .setButton {
    padding: 14px;
    margin-left: 60px;
    font-size: 1em;
    background: #000;
    color: #fff;
    border: 1px solid #000;
  }

  button:hover {
    color: #000;
    background: #fff;
  }

  [v-cloak] {
    opacity: 0;
    transition: all .3s;
  }

  label {
    width: 20%;
    padding: 10px 0;
    display: inline-block;
  }

  h1{
    font-size: 3em;
    text-align: center;
    
  }
  .timer {
    font-size: 7em;
    margin: 20px;
    position: center;
  }
</style>
