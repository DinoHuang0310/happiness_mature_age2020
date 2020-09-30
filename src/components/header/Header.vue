<template>
  <header>
    <ul>
      <li>
        <a href="https://www.businesstoday.com.tw/" target="_blank">
          <img class="businesstoday" src="../../assets/images/businesstoday.svg" alt="今周刊" />
        </a>
      </li>
      <li>
        <a href="http://thebetteraging.businesstoday.com.tw/" target="_blank">
          <img class="thebetteraging" src="../../assets/images/happiness_mature_age.png" alt="幸福熟齡" />
        </a>
      </li>
    </ul>
    <BtnetNavbar :navList="navList" />
  </header>
</template>

<script>
import BtnetNavbar from './BtnetNavbar.vue'
import IconFB from '../../assets/images/ico-facebook.svg'
import IconLine from '../../assets/images/ico-line.svg'

export default {
  components: {
    BtnetNavbar,
  },
  data: function() {
    return {
      navList: [
        {
          name: "首頁",
          url: "#kv_area",
          isAnchor: true,
        },
        {
          name: "引言",
          url: "#about",
          isAnchor: true,
        },
        {
          name: "講者",
          url: "#speakers",
          isAnchor: true,
        },
        {
          name: "議程",
          url: "#agenda",
          isAnchor: true,
        },
        {
          name: "立即報名",
          url: "#register",
          isAnchor: true,
        },
        {
          name: "參展夥伴",
          url: "#exhibitor",
          isAnchor: true,
        },
        {
          name: "特別企劃",
          url: "#report",
          isAnchor: true,
        },
        {
          name: "精彩回顧",
          navList: [
            {
              name: "2017",
              url: "https://event.businesstoday.com.tw/2017/happyelderlyforum/"
            },
            {
              name: "2018",
              url: "https://event.businesstoday.com.tw/2018/happiness_mature_age/"
            },
            {
              name: "2019",
              url: "https://events.businesstoday.com.tw/2019/happiness_mature_age/"
            }
          ]
        },
        {
          name: `<img src="${IconFB}" alt="facebook-share" />`,
          class: "facebook-share",
          url: "http://www.facebook.com/share.php?u=https://events.businesstoday.com.tw/2020/happiness_mature_age/",
          isAnchor: false,
        },
        {
          name: `<img src="${IconLine}" alt="line-share" />`,
          class: "line-share",
          url: "https://social-plugins.line.me/lineit/share?url=https://events.businesstoday.com.tw/2020/happiness_mature_age/",
          isAnchor: false,
        }
      ]
    }
  }
}
</script>

<style>
header {
    position: fixed;
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    top: 0;
    left: 0;
    background: rgba(255, 255, 255, .5);
    z-index: 99;
}
header > ul {
  display: flex;
}
header > ul li {
  margin: 0.4em;
}
header img {
  display: block;
}
.businesstoday {
  width: 80px;
}
.thebetteraging {
  width: 140px;
}

@media screen and (max-width: 1024px) {
  
}

@media screen and (max-width: 640px) {
  .businesstoday {
    width: 60px;
  }
  .thebetteraging {
    width: 100px;
  }
}

@media screen and (max-width: 480px) {
  
}

</style>
