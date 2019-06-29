<template>
  <div class="tools">
    <input type="file" v-on:change="handleImageUpload" accept="image/*" />
    <div>
      Hand Color: <input type="color" v-on:change="changeHandColor" v-bind:value="currentHandColor" />
    </div>
    <div>
      Face Color: <input type="color" v-on:change="changeFaceColor" v-bind:value="currentFaceColor" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'Tools',
  props: {
    handColor: String,
    faceColor: String
  },
  data: function () {
    return {
      currentHandColor: this.handColor,
      currentFaceColor: this.faceColor
    }
  },
  methods: {
    handleImageUpload: function (e) {
      const reader = new FileReader();
      reader.onload = (read) => {
        this.$root.$emit('change-background', read.target.result);
      }
      reader.readAsDataURL(e.srcElement.files[0]);
    },
    changeHandColor: function (e) {
      this.$root.$emit('change-hand', e.srcElement.value);
    },
    changeFaceColor: function (e) {
      this.$root.$emit('change-face', e.srcElement.value);
    }
  }
}
</script>

<style>
.tools {
  width: 500px;
  margin: 20px auto;
  position: relative;
  text-align: left;
}
</style>
