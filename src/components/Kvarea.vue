<template>
  <div id="kv_area" ref="infoBox">
    <Point :windowWidth="boxWidth" :windowHeight="boxHeight" :draw="animated" />
    <picture>
      <source media="(min-width: 481px)" srcset="../assets/images/cloud_2.png">
      <source media="(max-width: 480px)" srcset="../assets/images/cloud_2_m.png">
      <img class="cloud" src="../assets/images/cloud_2.png" alt="" @load="imgLoaded">
    </picture>
    <div :class="animated ? 'chara_area animate' : 'chara_area'">
      <img id="characters_left1" :class="animated ? 'animate' : null" src="../assets/images/characters_left1.png" alt="" @load="imgLoaded">
      <img id="characters_left2" :class="animated ? 'animate' : null" src="../assets/images/characters_left2.png" alt="" @load="imgLoaded">
      <img id="characters_right2" :class="animated ? 'animate' : null" src="../assets/images/characters_right2.png" alt="" @load="imgLoaded">
      <img id="characters_right1" :class="animated ? 'animate' : null" src="../assets/images/characters_right1.png" alt="" @load="imgLoaded">
      <img id="characters_center" src="../assets/images/characters_center.png" alt="" @load="setViewBox">
    </div>
    <img class="cloud" id="cloud1" src="../assets/images/cloud_1.png" alt="" @load="imgLoaded">
    <figure>
      <h1>
        <img src="../assets/images/2020_happiness_mature_age.png" alt="幸福熟齡-高年級夢想家" @load="imgLoaded" />
      </h1>
      <figcaption>
        今周刊2020第四屆幸福熟齡臺日交流論壇
        <div>
          <mark>10月29日</mark>
          <span>格萊天漾大飯店15樓天闊廳</span>
        </div>
      </figcaption>
    </figure>
    <transition name="fade">
      <div class="loading" v-if="loading">
        <img src="../assets/images/loading.svg" alt="loading..." />
      </div>
    </transition>
  </div>
</template>

<script>
import Point from './Point'
export default {
  components: {
    Point
  },
  data() {
    return {
      loading: true,
      boxWidth: 0,
      boxHeight: 0,
      imgLoader: 0,
      animated: false
    }
  },
  methods: {
    setViewBox() {
      this.boxWidth = this.$refs.infoBox.clientWidth;
      this.boxHeight = this.$refs.infoBox.clientHeight;
      this.imgLoaded();
    },
    imgLoaded() {
      this.imgLoader = this.imgLoader + 1;
      if(this.imgLoader >= 7) {
        setTimeout(() => {
          this.loading = false;
          this.animated = true;
        }, 500);
      }
    }
  }
}
</script>

<style>
#kv_area {
  position: relative;
  background: linear-gradient(to top, #c2e9fb 0%, #8dbdfd 100%);
  overflow: hidden;
  text-align: center;
}
#kv_area img {
  display: block;
  width: 100%;
}
.chara_area {
  position: relative;
  display: inline-block;
  width: 32%;
  padding: 7% 0;
  transform: translate(0, 100%);
  -webkit-transition: all 600ms cubic-bezier(0.175, 0.885, 0.320, 1);
  -webkit-transition: all 600ms cubic-bezier(0.175, 0.885, 0.320, 1.275);
  -moz-transition: all 600ms cubic-bezier(0.175, 0.885, 0.320, 1.275);
  -o-transition: all 600ms cubic-bezier(0.175, 0.885, 0.320, 1.275);
  transition: all 600ms cubic-bezier(0.175, 0.885, 0.320, 1.275);
}
.chara_area img {
  position: absolute;
  left: 0;
  opacity: 0;
  transition: .5s;
}
#characters_center {
  position: relative;
  opacity: 1;
}
.chara_area img.animate {
  opacity: 1;
}
.chara_area.animate {
  transform: translate(0, 0);
}
#characters_left1.animate {
  transform: translate(-80%, 0);
}
#characters_left2.animate {
  transform: translate(-30%, 0);
}
#characters_right1.animate {
  transform: translate(30%, 0);
}
#characters_right2.animate {
  transform: translate(75%, 0);
}
.chara_area img.animate {
  transition-delay: 0.9s;
  -moz-transition-delay: 0.9s;
  -webkit-transition-delay: 0.9s;
  -o-transition-delay: 0.9s;
}
#kv_area h1,
#kv_area h1 img {
  position: relative;
}
#kv_area h1::before {
  content: '';
  width: 20%;
  height: 12%;
  position: absolute;
  bottom: 0;
  left: 50%;
  background-image: radial-gradient(closest-side, rgba(0, 0, 0, 0.5) 0, rgba(0, 0, 0, 0.2) 40%, transparent 100%);
  transform: translate(-50%, 6%);
}
.cloud {
  position: absolute;
  width: 100%;
  min-width: 100%;
  left: 0;
  bottom: 0;
}
#kv_area figure {
  position: absolute;
  width: 50%;
  bottom: 3%;
  left: 50%;
  transform: translate(-50%, 0);
  text-align: center;
}
#kv_area figcaption {
  position: relative;
  display: inline-block;
  font-size: 1.5vw;
  font-weight: 600;
  white-space: nowrap;
}
#kv_area figcaption div {
  display: flex;
  align-items: center;
  font-size: 1vw;
  font-weight: 400;
}
#kv_area figcaption div mark {
  color: white;
  background: #505050;
  padding: 0.2em 0.6em;
}
#kv_area figcaption div span {
  margin: 0 0.5em;
  letter-spacing: 0.2em;
}
#kv_area figcaption div::after {
  content: '';
  display: block;
  border-bottom: solid 1px #505050;
  flex: 1;
}
.loading {
  position: fixed;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  background: linear-gradient(to top, #c2e9fb 0%, #8dbdfd 100%);
  z-index: 999;
}
#kv_area .loading img {
  display: inline-block;
  width: 50px;
  height: 50px;
  -webkit-animation: setRotate 2s linear infinite;
  -moz-animation: setRotate 2s linear infinite;
  animation: setRotate 2s linear infinite;
}

@media screen and (max-width: 1280px) {
  #kv_area figcaption {
    font-size: 2vw;
  }
  #kv_area figcaption div {
    font-size: 1.5vw;
  }
}

@media screen and (max-width: 768px) {
  #kv_area figcaption {
    font-size: 2.5vw;
  }
  #kv_area figcaption div {
    font-size: 2vw;
  }
}

/* table only */
@media screen and (min-width: 768px) and (orientation: portrait) {
  .chara_area {
    width: 40%;
    padding: 13% 0 7%;
  }
}

/* mobile only */
@media screen and (max-width: 480px) and (orientation: portrait) {
  #kv_area {
    min-height: 90vh;
  }
}

@media screen and (max-width: 480px) {
  .chara_area {
    width: 90%;
    padding: 40% 0 5%;
  }
  #characters_left1.animate {
    transform: translate(-35%, -27%);
  }
  #characters_right2.animate {
    transform: translate(25%, -25%);
  }
  #cloud1.cloud {
    max-width: none;
    width: 200%;
  }
  #kv_area figure {
    width: 102%;
    bottom: 6%;
  }
  #kv_area figcaption {
    font-size: 5vw;
  }
  #kv_area figcaption div {
    font-size: 4vw;
  }
  #kv_area figcaption div span {
    letter-spacing: 0.1em;
  }
}

</style>
