<template>
  <div id="about" class="area color-area" ref="infoBox">
    <Point :windowWidth="boxWidth" :windowHeight="boxHeight" :draw="true" />
    <div class="wrapper">
      <div class="title">
        <h2><span>引</span>言</h2>
      </div>
      <div v-html="about" />
    </div>
  </div>
</template>

<script>
import Point from './Point'
export default {
  components: {
    Point
  },
  props: {
    about: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      boxWidth: 0,
      boxHeight: 0
    }
  },
  methods: {
    setViewBox() {
      this.boxWidth = this.$refs.infoBox.clientWidth;
      this.boxHeight = this.$refs.infoBox.clientHeight;
    }
  },
  mounted() {
    this.setViewBox();
  }
}
</script>

<style>
#about {
  position: relative;
  text-align: center;
}
</style>
