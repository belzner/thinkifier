<template>
  <div class="tools">
    <input id="upload" type="file" v-on:change="handleImageUpload" accept="image/*" />
  </div>
</template>

<script>
export default {
  name: 'Tools',
  methods: {
    handleImageUpload: function (e) {
      const reader = new FileReader();
      reader.onload = (read) => {
        this.$root.$emit('change-background', read.target.result);
      }
      reader.readAsDataURL(e.srcElement.files[0]);
    }
  }
}
</script>

<style>
.tools {
  margin: 20px auto;
  position: relative;
  text-align: center;
}
</style>
