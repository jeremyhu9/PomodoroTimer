<template>
  <div class="main">
    <h1>Pomodoro Timer</h1>
    <div class="instruction-container">
      <span>Instructions</span>
      <ol>
        <li>First 4 sessions are 25 minutes</li>
        <li>After each session, take a 5 minute break</li>
        <li>After you finish 4 counts, take a 15 minute break</li>
        <li>Repeat Step 1</li>
      </ol>
    </div>

    <div class="counter-container">
      <Counter v-bind:count="this.count"></Counter>
    </div>
    <div class="btn-container">
      <button class="button-container" @click="this.increment">START</button>
      <button class="button-container" @click="this.reset">Reset</button>
      <button class="button-container" @click="takeBreak('short')" v-if="countedOnce">Short Break</button>
      <button class="button-container" @click="takeBreak('long')" v-if="fourCounts">Long Break</button>
    </div>
    <div class="lightbox" v-bind:class="{'lightbox-inactive': !isActive}">
      <Timer v-bind:time="this.time"></Timer>
      <button class="button-container" v-on:click="this.stop">STOP</button>
    </div>
    <div class="lightbox" v-bind:class="{'breakbox-inactive': hideBreakBox}" style="background: #c7fc4b">
      <Timer v-bind:time="this.time"></Timer>
    </div>
  </div>
</template>


<script>
import Timer from './Timer'
import Counter from './Counter'

export default {
  name: 'landing',
  data () {
    return {
      count: 0,
      time: {
        minutes: 25,
        seconds: 60
      },
      start: false,
      countingDown: null,
      isActive: false,
      hideBreakBox: true,
      countedOnce: false,
      fourCounts: false
    }
  },
  components: {
    Timer,
    Counter,
  },
  methods: {
    increment () {
      if (this.count === 4) {
        this.count = 0;
        this.fourCounts = true;
      }
      this.count++;
      this.countDown();
      this.isActive = true;
      this.countedOnce = true;
    },
    countDown () {
      this.countingDown = setInterval(this.setTime, 1000)
    },
    setTime () {
      if (this.time.seconds === '00') {
        this.time.seconds = 60
        this.time.minutes--
      }

      if (this.time.minutes === -1) {
        clearInterval(this.countingDown);
        this.isActive = false
        this.hideBreakBox = true
        this.time.minutes = 25
      }

      this.time.seconds--

      if (this.time.seconds < 10 && this.time.seconds > 0) {
        this.time.seconds = '0' + this.time.seconds
      }
      // Subtracts minute when 60 seconds gone by
      if (this.time.seconds === 0) {
        this.time.seconds = '00'
      }


    },
    stop () {
      clearInterval(this.countingDown);
      this.time.minutes = 25
      this.time.seconds = "00"
      this.count = 0
      this.isActive = false;
      this.countedOnce = false;
    },
    reset () {
      this.time.seconds = 60
      this.time.minutes = 25
      this.count = 0
    },
    takeBreak (duration) {
      if(duration === "short") {
        this.time.minutes = 5
      } else {
        this.time.minutes = 15
      }

      this.hideBreakBox = false
      this.countDown();
    }
  }
}

</script>
