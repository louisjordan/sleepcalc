<template>
  <div id="app">
    <div class="page-content">
      <sleep-calc class="sleep-calc"></sleep-calc>
    </div>
  </div>
</template>

<script>
import SleepCalc from './SleepCalc.vue';

export default {
  name: 'app',
  data() {
    return {}
  },
  components: {
    'sleep-calc': SleepCalc
  }
}
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}

html,
body {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
}

#app {
  height: 100%;
  font-family: Helvetica, sans-serif;
  font-weight: 200;
  font-size: 1.3em;
}

body {
  animation: gradientAnimation 100s alternate infinite;
  background-size: 750% 750%;
  background-color: #304b80;
  background-image: -moz-linear-gradient(-45deg, #304b80, #80304b, #4b8030, #80304b, #304b80);
  background-image: -webkit-gradient(-45deg, #304b80, #80304b, #4b8030, #80304b, #304b80);
  background-image: -webkit-linear-gradient(-45deg, #304b80, #80304b, #4b8030, #80304b, #304b80);
  background-image: -o-linear-gradient(-45deg, #304b80, #80304b, #4b8030, #80304b, #304b80);
  background-image: -ms-linear-gradient(-45deg, #304b80, #80304b, #4b8030, #80304b, #304b80);
  background-image: linear-gradient(-45deg, #304b80, #80304b, #4b8030, #80304b, #304b80);
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#304b80', endColorstr='#4b8030', GradientType=1);
}

@keyframes gradientAnimation {
  0% {
    background-position: 0 0;
  }
  100% {
    background-position: 100% 100%;
  }
}

input,
button {
  font-family: Helvetica, sans-serif;
  font-weight: 200;
}

.page-content {
  height: 100vh;
  box-sizing: border-box;
  display: flex;
  flex-flow: row nowrap;
  justify-content: center;
  align-items: center;
}

.sleep-calc {
  width: 100%;
  max-width: 400px;
  min-height: 350px;
  margin: 5vw;
}

a {
  color: #42b983;
}
</style>
