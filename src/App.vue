<template>
  <div id="app">
    <img id="logo" alt="Thinkifier" src="./assets/thinking-face.svg">
    <Workspace v-bind:handColor="handColor" v-bind:faceColor="faceColor"></Workspace>
    <Tools v-bind:handColor="handColor" v-bind:faceColor="faceColor"></Tools>
  </div>
</template>

<script>
import Workspace from './components/Workspace.vue'
import Tools from './components/Tools.vue'

export default {
  name: 'app',
  components: {
    Workspace,
    Tools
  },
  data: function () {
    return {
      handColor: '#F19020',
      faceColor: '#65471B'
    }
  },
  mounted () {
    this.$root.$on('change-hand', this.changeHandColor);
    this.$root.$on('change-face', this.changeFaceColor);
  },
  methods: {
    changeHandColor: function (e) {
      this.handColor = e;
    },
    changeFaceColor: function (e) {
      this.faceColor = e;
    }
  }
}
</script>

<style>
#app {
  text-align: center;
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: #d0dff7;
}

#logo {
  margin: 30px 0;
  position: relative;
  width: 100px;
}
</style>
