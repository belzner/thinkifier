<template>
  <div class="feature" v-bind:class="{ active: isActive }" v-bind:style="{ top: top+'px', left: left+'px' }">
    <svg id="hand" v-if="type === 'hand'" xmlns="http://www.w3.org/2000/svg" viewBox="6.3 17.7 18.6 18.3" v-bind:width="width+'px'" v-bind:height="height+'px'" v-bind:x="left/5+'%'" v-bind:y="top/5+'%'">
      <path v-on:click.stop="setActive" v-bind:fill="handColor" d="M17.276 35.149s1.265-.411 1.429-1.352c.173-.972-.624-1.167-.624-1.167s1.041-.208 1.172-1.376c.123-1.101-.861-1.363-.861-1.363s.97-.4 1.016-1.539c.038-.959-.995-1.428-.995-1.428s5.038-1.221 5.556-1.341c.516-.12 1.32-.615 1.069-1.694-.249-1.08-1.204-1.118-1.697-1.003-.494.115-6.744 1.566-8.9 2.068l-1.439.334c-.54.127-.785-.11-.404-.512.508-.536.833-1.129.946-2.113.119-1.035-.232-2.313-.433-2.809-.374-.921-1.005-1.649-1.734-1.899-1.137-.39-1.945.321-1.542 1.561.604 1.854.208 3.375-.833 4.293-2.449 2.157-3.588 3.695-2.83 6.973.828 3.575 4.377 5.876 7.952 5.048l3.152-.681z"/>
    </svg>
    <svg id="right-eye" v-if="type === 'right-eye'" xmlns="http://www.w3.org/2000/svg" viewBox="12.5 1.5 7.3 7.7" v-bind:width="width+'px'" v-bind:height="height+'px'" v-bind:x="left/5+'%'" v-bind:y="top/5+'%'">
      <ellipse v-on:click.stop="setActive" v-bind:fill="faceColor" cx="15.375" cy="5.937" rx="2.125" ry="2.656"/>
      <path v-on:click.stop="setActive" v-bind:fill="faceColor" d="M12.135 3.75c-.156-.098-.286-.243-.362-.424-.187-.442.023-.927.468-1.084 4.381-1.536 7.685.48 7.823.567.415.26.555.787.312 1.178-.242.39-.776.495-1.191.238-.12-.072-2.727-1.621-6.267-.379-.266.091-.553.046-.783-.096z"/>
    </svg>
    <svg id="left-eye" v-if="type === 'left-eye'" xmlns="http://www.w3.org/2000/svg" viewBox="8.7 4.1 9.2 9.5" v-bind:width="width+'px'" v-bind:height="height+'px'" v-bind:x="left/5+'%'" v-bind:y="top/5+'%'">
      <ellipse v-on:click.stop="setActive" v-bind:fill="faceColor" cx="13.119" cy="11.174" rx="2.125" ry="2.656"/>
      <path v-on:click.stop="setActive" v-bind:fill="faceColor" d="M9.296 6.351c-.164-.088-.303-.224-.391-.399-.216-.428-.04-.927.393-1.112 4.266-1.831 7.699-.043 7.843.034.433.231.608.747.391 1.154-.216.405-.74.546-1.173.318-.123-.063-2.832-1.432-6.278.047-.257.109-.547.085-.785-.042z"/>
    </svg>
    <svg id="mouth" v-if="type === 'mouth'" xmlns="http://www.w3.org/2000/svg" viewBox="16.8 19 3.5 3.5" v-bind:width="width+'px'" v-bind:height="height+'px'" v-bind:x="left/5+'%'" v-bind:y="top/5+'%'">
      <path v-on:click.stop="setActive" v-bind:fill="faceColor" d="M14.524 21.036c-.145-.116-.258-.274-.312-.464-.134-.46.13-.918.59-1.021 4.528-1.021 7.577 1.363 7.706 1.465.384.306.459.845.173 1.205-.286.358-.828.401-1.211.097-.11-.084-2.523-1.923-6.182-1.098-.274.061-.554-.016-.764-.184z"/>
    </svg>
    <div class="move-tab" v-on:dragstart="startDrag" v-on:dragend="endDrag" v-on:drag="moving" draggable="true"></div>
    <div class="pull-tab" v-on:dragstart="startDrag" v-on:dragend="endDrag" v-on:drag="resizing" draggable="true"></div>
  </div>
</template>

<script>
export default {
  name: 'Feature',
  props: {
    type: String,
    workspaceSize: Number,
    initValues: Object,
    handColor: String,
    faceColor: String
  },
  data: function () {
    return {
      isActive: false,
      startX: null,
      startY: null,
      startTop: null,
      startLeft: null,
      startWidth: null,
      startHeight: null,
      top: this.initValues.top,
      left: this.initValues.left,
      width: this.initValues.width,
      height: this.initValues.height
    }
  },
  mounted () {
    this.$root.$on('remove-active', this.removeActive);
  },
  methods: {
    setActive: function () {
      this.$root.$emit('remove-active');
      this.isActive = true;
    },
    removeActive: function () {
      this.isActive = false;
    },
    startDrag: function (e) {
      this.startX = e.x;
      this.startY = e.y;
      this.startTop = this.top;
      this.startLeft = this.left;
      this.startWidth = this.width;
      this.startHeight = this.height;
    },
    endDrag: function () {
      this.startX = null;
      this.startY = null;
      this.startTop = null;
      this.startLeft = null;
      this.startWidth = null;
      this.startHeight = null;
    },
    moving: function (e) {
      const newTop = this.startTop + (e.y - this.startY);
      if (newTop >= 0 && newTop <= this.workspaceSize - this.height) {
        this.top = newTop;
      }

      const newLeft = this.startLeft + (e.x - this.startX);
      if (newLeft >= 0 && newLeft <= this.workspaceSize - this.width) {
        this.left = newLeft;
      }
    },
    resizing: function (e) {
      const ratio = this.startHeight / this.startWidth;
      const newWidth = this.startWidth + Math.min(e.x - this.startX, e.y - this.startY);
      const newHeight = newWidth * ratio;
      if (newWidth >= 20 && newHeight + this.top <= this.workspaceSize && newWidth + this.left <= this.workspaceSize) {
        this.width = newWidth;
        this.height = newHeight;
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.feature {
  position: absolute;
  pointer-events: none;
}

.feature path, .feature ellipse {
  pointer-events: auto;
}

.active {
  margin-top: -1px;
  margin-left: -1px;
  border: 1px solid #000000;
}

.move-tab, .pull-tab {
  box-sizing: border-box;
  pointer-events: auto;
  position: absolute;
  border: 1px solid #000000;
  background-color: #ffffff;
  width: 10px;
  height: 10px;
  display: none;
}

.active .move-tab, .active .pull-tab {
  display: block;
}

.move-tab {
  top: 5px;
  left: 5px;
  cursor: move;
}

.pull-tab {
  bottom: -5px;
  right: -5px;
  cursor: nwse-resize;
}
</style>
