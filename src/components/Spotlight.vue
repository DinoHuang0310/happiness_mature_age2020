<template>
  <div id="spotlight" class="area" ref="spotlight" v-if="spotlight.length">
    <div class="wrapper">
      <div class="title">
        <h2><span>論壇亮</span>點</h2>
      </div>
      <ul class="spotlight">
        <li
          v-for="(list, index) in spotlight"
          :key="list.index"
        >
          <h3>
            <ICountUp
              :delay="delay"
              :endVal="endVal[index]"
              :options="options"
            />{{ list.unit }}
          </h3>
          <div v-html="list.description" />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import ICountUp from 'vue-countup-v2';
export default {
  components: {
    ICountUp
  },
  props: {
    spotlight: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      // windowWidth: null,
      delay: 500,
      endVal: [0, 0, 0],
      options: {
        useEasing: true,
        useGrouping: true,
        duration: 1.5, // 持續時間
        separator: '', // 千位分隔符 ex: ','
        decimal: '.',
        prefix: '',
        suffix: ''
      }
    }
  },
  methods: {
    handleScroll() {
      const startPoint = document.documentElement.clientHeight * 0.8;
      const scrollTop = this.scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
      if(scrollTop + startPoint > this.$refs.spotlight.offsetTop) {
        this.endVal = [
          this.spotlight[0].val,
          this.spotlight[1].val,
          this.spotlight[2].val
        ];
      } else {
        // reset
        this.endVal = [0, 0, 0];
      }
    },
    // checkScreen() {
    //   const clientWidth = document.documentElement.clientWidth;
    //   if(clientWidth !== this.windowWidth) {
    //     this.windowWidth = clientWidth;
    //   }
    // }
  },
  mounted() {
    if(this.spotlight.length) window.addEventListener('scroll', this.handleScroll, false);
    
    // window.addEventListener('resize', this.checkScreen);
    // this.checkScreen();
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.handleScroll);
    // window.removeEventListener('resize', this.checkScreen);
  },
}
</script>

<style>
.spotlight {
  display: flex;
  justify-content: space-between;
  text-align: center;
  margin-top: 5em;
}
.spotlight > li {
  position: relative;
  width: 30%;
  background: #f09819;
  color: white;
  letter-spacing: 0.2em;
  padding: 3em 1em;
}
.spotlight > li h3 {
  position: absolute;
  margin: 0;
  color: #f09819;
  top: 0;
  left: 50%;
  transform: translate(-50%, -85%);
  white-space: nowrap;
}
.spotlight > li h3 span {
  font-family: 'Roboto Mono', monospace;
  font-size: 3vw;
  display: inline-block;
}
#spotlight .d-roll-wrapper {
  margin: 0;
}

@media screen and (max-width: 1280px) {
  .spotlight > li h3 span {
    font-size: 4vw;
  }
}

@media screen and (max-width: 768px) {
  .spotlight > li h3 span {
    font-size: 5vw;
  }
}

@media screen and (max-width: 640px) {
  .spotlight {
    flex-wrap: wrap;
    justify-content: center;
    margin-top: 1.5em;
  }
  .spotlight > li {
    width: 80%;
  }
}

@media screen and (max-width: 480px) {
  .spotlight > li {
    width: 90%;
    margin: 2.5em 0;
  }
  .spotlight > li h3 span {
    font-size: 12vw;
  }
}

</style>
