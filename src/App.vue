<template>
  <div id="app">
    <svg id="head" viewBox="0 0 500 500" width="200">
      <image id="cur-background" v-bind:href="background" width="256" height="256" x="122" y="122" />
      <use href="#left-eye" />
      <use href="#right-eye" />
      <use href="#mouth" />
      <use href="#hand" />
    </svg>
    <Workspace v-bind:handColor="handColor" v-bind:faceColor="faceColor" v-bind:background="background"></Workspace>
    <Tools v-bind:handColor="handColor" v-bind:faceColor="faceColor"></Tools>
    <button v-on:click="saveImage">Download</button>
    <div class="about">
      <p>Apply thinky-face features to any image. You can click on the hand, eyes, or mouth to move (upper left) and resize (lower right) them. Change background image and colors above. "Download" button to save.</p>
      <p>Thinking face emoji graphic from <a href="https://github.com/twitter/twemoji">Twemoji</a>, licensed under <a href="https://creativecommons.org/licenses/by/4.0/">CC-BY 4.0</a></p>
      <p>Code by <a href="https://github.com/belzner">Megan Belzner</a></p>
    </div>
    <div class="hidden">
      <svg id="svg" viewBox="0 0 500 500" width="200"></svg>
      <canvas id="canvas" width="200" height="200"></canvas>
    </div>
  </div>
</template>

<script>
import Workspace from './components/Workspace.vue'
import Tools from './components/Tools.vue'
import Background from './assets/face-circle.svg'

export default {
  name: 'app',
  components: {
    Workspace,
    Tools
  },
  data: function () {
    return {
      handColor: '#F19020',
      faceColor: '#65471B',
      background: Background
    }
  },
  mounted () {
    this.$root.$on('change-hand', this.changeHandColor);
    this.$root.$on('change-face', this.changeFaceColor);
    this.$root.$on('change-background', this.changeBackground);
  },
  methods: {
    changeHandColor: function (e) {
      this.handColor = e;
    },
    changeFaceColor: function (e) {
      this.faceColor = e;
    },
    changeBackground: function (e) {
      this.background = e;
    },
    saveImage: function () {
      const svg = document.getElementById('svg');
      svg.innerHTML = '';
      svg.appendChild(document.getElementById('left-eye').cloneNode(true));
      svg.appendChild(document.getElementById('right-eye').cloneNode(true));
      svg.appendChild(document.getElementById('mouth').cloneNode(true));
      svg.appendChild(document.getElementById('hand').cloneNode(true));

      const background = document.getElementById('cur-background');
      const canvas = document.getElementById('canvas');
      canvas.getContext('2d').clearRect(0, 0, canvas.width, canvas.height);
      canvas.getContext('2d').drawImage(background, 48.8, 48.8, 102.4, 102.4);

      // See https://jsfiddle.net/Wijmo5/h2L3gw88/
      const xml = new XMLSerializer().serializeToString(svg);
      const svg64 = btoa(xml);
      const b64Start = 'data:image/svg+xml;base64,';
      const image64 = b64Start + svg64;

      const img = new Image();
      img.addEventListener('load', () => {
        canvas.getContext('2d').drawImage(img, 0, 0);

        const link = document.createElement('a');
        const dataURL = canvas.toDataURL('image/png').replace("image/png", "image/octet-stream");
        link.download = 'thinky.png';
        link.href = dataURL;
        link.click();
      }, false);
      img.src = image64;
    }
  }
}
</script>

<style>
body {
  margin: 0;
}

#app {
  text-align: center;
  min-height: 100vh;
  background-color: #d0dff7;
  font-family: Arial, Helvetica, sans-serif;
}

#logo {
  margin: 30px 0;
  position: relative;
  width: 100px;
}

.about {
  margin: 0 auto;
  padding-bottom: 20px;
  position: relative;
  width: 500px;
}

.hidden {
  display: none;
}
</style>
