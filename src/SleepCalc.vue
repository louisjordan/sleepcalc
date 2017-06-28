<template>
  <div class="container">
  
    <p>
      <button @click="mode = mode === 'wakeupat' ? 'fallasleepat' : 'wakeupat'">Toggle</button>
    </p>
  
    <p>
      If I want to
      <b v-if="mode === 'wakeupat'">wake up</b>
      <b v-else>fall asleep</b>
      at
    </p>
  
    <input v-model="hours" type="number" max="24" min="-1"> :
    <input v-model="minutes" type="number" max="60" min="-15" step="15">
    <button v-show="mode === 'fallasleepat'" @click="setTime">Now</button>
  
    <p>
      I should
      <b v-if="mode === 'wakeupat'">fall asleep</b>
      <b v-else>wake up</b>
      at
    </p>
  
    <ul>
      <li v-for="(time, index) in times" :key="index">{{ time }}</li>
    </ul>
  
  </div>
</template>

<script>
function formatTime(time) {
  time = new Date(time);

  let hours = time.getHours();
  hours = hours > 9 ? hours : `0${hours}`;

  let minutes = time.getMinutes();
  minutes = minutes > 9 ? minutes : `0${minutes}`;

  return `${hours}:${minutes}`
}

function calculateWakeIntervals(time, forward = true) {
  let intervals = [];

  for (var i = 1; i <= 7; i++) {
    let interval = 1000 * 60 * 90 * i;
    intervals.push(formatTime(forward ? time + interval : time - interval));
  }

  return forward ? intervals.reverse() : intervals;
}

function padLeft(input, maxLength, padCharacter) {
  input = String(input);
  if (input) {
    const paddingLength = maxLength - input.length;
    const padding = new Array(paddingLength).fill(padCharacter);
    return padding.join('') + input;
  }
}

export default {
  name: 'sleep-calc',
  data() {
    return {
      mode: 'wakeupat',
      hours: '08',
      minutes: '00',
      time: ''
    }
  },
  updated() {
    const hours = Number(this.hours);
    const minutes = Number(this.minutes);

    if (minutes <= -1) {
      this.minutes = 45;
      this.hours = hours - 1;
    } else if (minutes >= 60) {
      this.minutes = 0;
      this.hours = hours + 1;
    }

    if (this.hours <= -1) {
      this.hours = 23;
    } else if (this.hours >= 24) {
      this.hours = 0;
    }

    this.minutes = padLeft(this.minutes, 2, '0');
  },
  computed: {
    times() {
      const currentTime = new Date(1970, 0, 1, this.hours, this.minutes || 0).getTime();
      return calculateWakeIntervals(currentTime, this.mode === 'fallasleepat');
    }
  },
  methods: {
    setTime() {
      const now = formatTime(Date.now()).split(':');
      this.hours = now[0];
      this.minutes = now[1];
    }
  }
}
</script>

<style lang="scss">
.container {
  text-align: center;
  background: rgba(0, 0, 0, 0.1);
  padding: 32px;
  color: white;
  opacity: 0.8;
}

input {
  color: white;
  background: none;
  text-align: center;
  border: 0;
  outline: 0;
  border-bottom: 2px solid white;
  border-radius: 0;
}

button {
  background: rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  color: white;
  border: 0;
  outline: 0;
  padding: 5px 10px;
  transition: 0.3s ease;
  cursor: pointer;
}

button:hover {
  background: rgba(0, 0, 0, 0.4);
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 8px;
  background: rgba(0, 0, 0, 0.2);
  padding: 8px 16px;
  border-radius: 3px;
}
</style>
