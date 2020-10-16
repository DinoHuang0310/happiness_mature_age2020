<template>
  <div id="exhibitor" class="area" v-if="exhibitor.length">
    <div class="content">
      <div class="title">
        <h2><span>參展夥</span>伴</h2>
      </div>
      <ul>
        <Exhibitor
           v-for="(list, index) in exhibitor"
          :key="index"
          :exhibitor="list"
          :isMobile="isMobile"
        />
      </ul>
    </div>
  </div>
</template>

<script>
import Exhibitor from './ExhibitorList'
export default {
  components: {
    Exhibitor
  },
  props: {
    exhibitor: {
      type: Array,
      required: true
    },
    isMobile: {
      type: Boolean,
      required: true
    }
  }
}
</script>

<style>
#exhibitor ul {
  display: flex;
  flex-wrap: wrap;
}

@media screen and (max-width: 480px) {
  #exhibitor ul {
    width: 90%;
    margin: auto;
  }
}

</style>
