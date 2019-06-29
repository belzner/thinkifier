<template>
  <div id="app">
    <img id="logo" alt="Thinkifier" src="./assets/thinking-face.svg">
    <Workspace></Workspace>
    <Tools></Tools>
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
