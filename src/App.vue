<template>
  <div id="app">
    <button v-on:click="recognize">recognize</button>
    <img id="text-img" alt="Vue logo" src="./assets/testocr.png">
  </div>
</template>

<script>
/* eslint-disable */
import { createWorker, PSM, OEM } from 'tesseract.js';
const worker = createWorker({
  logger: m => console.log(m),
});

export default {
  name: 'app',
  methods: {
    recognize: async () => {
      const img = document.getElementById('text-img');
      console.log(img);
      await worker.load();
      await worker.loadLanguage('eng');
      await worker.initialize('eng', OEM.LSTM_ONLY);
      await worker.setParameters({
        tessedit_pageseg_mode: PSM.SINGLE_BLOCK,
      });
      const { data: { text } } = await worker.recognize(img);
      console.log(text);
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
