<template>
  <div id="app">
    <svg id="head" viewBox="0 0 500 500" width="128">
      <image v-bind:href="background" width="256" height="256" x="122" y="122" />
      <use href="#left-eye" />
      <use href="#right-eye" />
      <use href="#mouth" />
      <use href="#hand" />
    </svg>
    <Workspace v-bind:handColor="handColor" v-bind:faceColor="faceColor" v-bind:background="background"></Workspace>
    <Tools v-bind:handColor="handColor" v-bind:faceColor="faceColor"></Tools>
    <div class="about">
      <p>Apply thinky-face features to any image. You can click on the hand, eyes, or mouth to move (upper left) and resize (lower right) them. Change background image and colors above. Screenshot to save.</p>
      <p>Thinking face emoji graphic from <a href="https://github.com/twitter/twemoji">Twemoji</a>, licensed under <a href="https://creativecommons.org/licenses/by/4.0/">CC-BY 4.0</a></p>
      <p>Code by <a href="https://github.com/belzner">Megan Belzner</a></p>
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
</style>
