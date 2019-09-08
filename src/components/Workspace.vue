<template>
  <div class="workspace" v-bind:style="{ width: size+'px', height: size+'px' }" v-on:click="$root.$emit('remove-active')" v-on:dragover.prevent="doNothing" v-on:drop.prevent="doNothing">
    <div class="background">
      <img v-bind:src="background"/>
    </div>
    <Feature type="left-eye" v-bind:workspace-size="size" v-bind:init-values="{ top: 150, left: 186, width: 65, height: 74 }" v-bind:handColor="handColor" v-bind:faceColor="faceColor"></Feature>
    <Feature type="right-eye" v-bind:workspace-size="size" v-bind:init-values="{ top: 178, left: 270, width: 64, height: 53 }" v-bind:handColor="handColor" v-bind:faceColor="faceColor"></Feature>
    <Feature type="mouth" v-bind:workspace-size="size" v-bind:init-values="{ top: 257, left: 219, width: 67, height: 25 }" v-bind:handColor="handColor" v-bind:faceColor="faceColor"></Feature>
    <Feature type="hand" v-bind:workspace-size="size" v-bind:init-values="{ top: 247, left: 165, width: 137, height: 130 }" v-bind:handColor="handColor" v-bind:faceColor="faceColor"></Feature>
  </div>
</template>

<script>
import Feature from './Feature.vue'

export default {
  name: 'Workspace',
  components: {
    Feature
  },
  props: {
    handColor: String,
    faceColor: String,
    background: String
  },
  data: function () {
    return {
      size: 500
    }
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
  background-color: #ffffff;
}

.background {
  width: 256px;
  position: relative;
  top: 122px;
  left: 122px;
}

.background img {
  width: 256px;
}
</style>
