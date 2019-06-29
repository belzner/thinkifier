<template>
  <div class="workspace" v-bind:style="{ width: size+'px', height: size+'px' }" v-on:click="$root.$emit('remove-active')" v-on:dragover.prevent="doNothing" v-on:drop.prevent="doNothing">
    <div class="background">
      <img v-bind:src="background"/>
    </div>
    <Feature type="left-eye" v-bind:workspace-size="size" v-bind:init-values="{ top: 144, left: 171, size: 86 }" v-bind:handColor="handColor" v-bind:faceColor="faceColor"></Feature>
    <Feature type="right-eye" v-bind:workspace-size="size" v-bind:init-values="{ top: 168, left: 265, size: 71 }" v-bind:handColor="handColor" v-bind:faceColor="faceColor"></Feature>
    <Feature type="mouth" v-bind:workspace-size="size" v-bind:init-values="{ top: 228, left: 206, size: 94 }" v-bind:handColor="handColor" v-bind:faceColor="faceColor"></Feature>
    <Feature type="hand" v-bind:workspace-size="size" v-bind:init-values="{ top: 242, left: 158, size: 150 }" v-bind:handColor="handColor" v-bind:faceColor="faceColor"></Feature>
  </div>
</template>

<script>
import Feature from './Feature.vue'
import Background from '../assets/face-circle.svg'

export default {
  name: 'Workspace',
  components: {
    Feature
  },
  props: {
    handColor: String,
    faceColor: String
  },
  data: function () {
    return {
      size: 500,
      background: Background
    }
  },
  mounted () {
    this.$root.$on('change-background', this.changeBackground);
  },
  methods: {
    doNothing: function () {},
    changeBackground: function (e) {
      this.background = e;
    }
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
