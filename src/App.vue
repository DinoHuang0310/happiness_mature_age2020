<template>
  <div id="app">
    <Kvarea />
    <Header />
    <About v-if="data" :about="data.about" />
    <Spotlight v-if="data" :spotlight="data.spotlight" />
    <Speakers v-if="data" :speakers="data.speakers" />
    <Information />
    <Agenda />
    <Register v-if="data" :formState="data.formState" />
    <Exhibitor v-if="data" :exhibitor="data.exhibitor" :isMobile="isMobile" />
    <Report v-if="data" :slider="data.slider" />
    <Organizer v-if="data" :agencys="data.agencys" />
    <BtnetFooter />
  </div>
</template>

<script>
import Header from './components/header/Header'
import Kvarea from './components/Kvarea'
import About from './components/About'
import Spotlight from './components/Spotlight'
import Speakers from './components/speakers/Speakers'
import Information from './components/Information'
import Agenda from './components/Agenda'
import Register from './components/Register'
import Exhibitor from './components/exhibitor/Exhibitor'
import Report from './components/report/Report'
import Organizer from './components/organizer/Organizer'
import BtnetFooter from './components/BtnetFooter'

import axios from 'axios'
// import AOS from 'aos';
// import 'aos/dist/aos.css';

export default {
  name: 'App',
  components: {
    Header,
    Kvarea,
    About,
    Spotlight,
    Speakers,
    Information,
    Agenda,
    Register,
    Exhibitor,
    Report,
    Organizer,
    BtnetFooter
  },
  data: function() {
    return {
      data: null,
      isMobile: true,
      windowWidth: null,
    }
  },
  methods: {
    checkScreen() {
      const clientWidth = document.documentElement.clientWidth;
      if(clientWidth !== this.windowWidth) {
        this.isMobile = /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent);
        this.windowWidth = clientWidth;
      }
    },
  },
  mounted() {
    axios.get(`data.json?${new Date().getTime()}`).then(response => {
      this.data = response.data;
      // AOS.init();
    }).catch(error => {
      console.log(error);
    });
    window.addEventListener('resize', this.checkScreen);
    this.checkScreen();
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.checkScreen);
  },
}
</script>

<style src='./assets/css/style.css'></style>
