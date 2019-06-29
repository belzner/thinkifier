<template>
  <div class="workspace" v-on:click="$root.$emit('remove-active')" v-on:dragover.prevent="doNothing" v-on:drop.prevent="doNothing">
    <div class="background">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 36 36">
        <circle fill="#FFCB4C" cx="18" cy="17.018" r="17"/>
      </svg>
    </div>
    <Feature type="left-eye"></Feature>
    <Feature type="right-eye"></Feature>
    <Feature type="mouth"></Feature>
    <Feature type="hand"></Feature>
  </div>
</template>

<script>
import Feature from './Feature.vue'

export default {
  name: 'Workspace',
  components: {
    Feature
  },
  methods: {
    doNothing: function () {}
  }
}
</script>

<style>
.workspace {
  margin: auto;
  position: relative;
  width: 500px;
  height: 500px;
  background-color: #ffffff;
}
.background {
  width: 256px;
  position: relative;
  top: 122px;
  left: 122px;
}
</style>
