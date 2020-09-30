<template>
  <div class="point">
    <div
      v-for="index in windowWidth > 480 ? 30 : 15"
      :key="index"
      :class="draw ? 'circle' : 'circle fixed'"
      :style="createCircle(index)"
    />
  </div>
</template>

<script>
export default {
  props: {
    windowHeight: {
      type: Number,
      required: true
    },
    windowWidth: {
      type: Number,
      required: true
    },
    draw: {
      type: Boolean,
      required: false
    },
  },
  methods: {
    getRandom(min, max, notInteger) {
      // notInteger為true 回傳至小數點後2位 以千位數為單位; ex: 400 -> 0.4, 1500 -> 1.5
      if(notInteger) {
        return (Math.floor(Math.random() * max) + min) * 0.001;
      }
      return Math.ceil(Math.random() * (max - min)) + min;
    },
    createCircle(index) {
      const size = this.getRandom(10, 25);
      const background = (index + 2) % 2 === 1 ? '#f09819' : '#ffffff';
      const x = this.getRandom((this.windowWidth / 2) * -1, (this.windowWidth / 2));
      const y = this.getRandom((this.windowHeight / 2) * -1, (this.windowHeight / 2));
      return `width: ${size}px; height: ${size}px; background: ${background}; transform: translate(${x}px, ${y}px);`;
    }
  }
}
</script>

<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity 1s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
.point {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  overflow: hidden;
}
.point .circle {
  position: absolute;
  border-radius: 50%;
  top: 50%;
  left: 50%;
  opacity: 1;
  transition: 1s;
}
.point .circle.fixed {
  opacity: 0;
  transform: translate(0, 0) !important;
}

@media screen and (max-width: 480px) {
  .point svg {
    opacity: .65;
  }
}
</style>
