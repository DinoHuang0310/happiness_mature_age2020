<template>
  <div id="report" class="area">
    <div class="title">
      <h2><span>特別企</span>劃</h2>
    </div>
    <div class="report-box" v-if="slider">
      <BtnetSlider :sliderData="slider" sliderName="slider" />
    </div>
  </div>
</template>

<script>
import BtnetSlider from './BtnetSlider'

export default {
  components: {
    BtnetSlider
  },
  props: {
    slider: {
      type: Array,
      required: false
    }
  }
}
</script>

<style>
#report {
  overflow: hidden;
}
.report-box {
  padding: 2em 2%;
}
.report-box h3 {
  text-align: center;
  font-size: 1.4em;
  margin: 0 0 0.5em;
}

</style>
