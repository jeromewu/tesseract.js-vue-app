<template>
  <div id="app">
    <button v-on:click="recognize">recognize</button>
    <img id="text-img" alt="Vue logo" src="./assets/testocr.png">
  </div>
</template>

<script>
/* eslint-disable */
import { TesseractWorker, PSM, OEM } from 'tesseract.js';
const worker = new TesseractWorker();

export default {
  name: 'app',
  methods: {
    recognize() {
      const img = document.getElementById('text-img');
      console.log(img);
      worker
        .recognize(img, 'eng', {
          tessedit_ocr_engine_mode: OEM.LSTM_ONLY,
          tessedit_pageseg_mode: PSM.SINGLE_BLOCK,
        })
        .then(result => {
          console.log(result);
        });
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
