<template>
  <div id="speakers" class="area">
    <div class="wrapper">
      <div class="title">
        <h2><span>講</span>者</h2>
        <p>*順序依議程表排列</p>
      </div>
      <ul class="other-speakers">
        <SpeakersDetails
          v-for="(list, index) in speakers"
          :key="index"
          :details="list"
          :myindex="index"
        />
      </ul>
    </div>
  </div>
</template>

<script>
import SpeakersDetails from './SpeakersDetails'

export default {
  components: {
    SpeakersDetails
  },
  props: {
    speakers: {
      type: Array,
      required: true
    }
  }
}
</script>

<style>
#speakers .content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
#speakers .content figure {
  width: 30%;
  color: #505050;
  text-align: center;
}
#speakers figure img {
  border-radius: 50%;
}
.speaker-position {
  width: 100%;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: normal;
}
#speakers h5 {
  font-size: 1.4em;
  margin: 0;
}
.main-speaker {
  width: 65%;
}
.main-speaker article {
  position: relative;
  padding: 1em;
  background: white;
  z-index: 1;
}
.main-speaker article h4 {
  display: inline-block;
  color: white;
  font-size: 1.2em;
  font-weight: 500;
  margin: 0;
  padding: 0.2em 0.8em;
  border-radius: 2em;
  background: #f09819;
}
.main-speaker article ul {
  padding-left: 1.5em;
}
.main-speaker article ul li {
  list-style-type: disc;
  color: #f09819;
}
.main-speaker article ul li p {
  color: #505050;
}
.other-speakers {
  display: flex;
  flex-wrap: wrap;
  margin-top: 2em;
}
.other-speakers > li {
  width: 22%;
  margin: 2% 1.5%;
  text-align: center;
}
.other-speakers img {
  width: 85%;
}
.other-speakers li button {
  color: white;
  font-size: inherit;
  font-weight: 500;
  letter-spacing: 0.1em;
  border: none;
  border-radius: 2em;
  background: #f09819;
  margin-top: 0.5em;
  padding: 0.3em 1.5em;
  opacity: 1;
  transition: .5s;
}
.vm--top-right-slot button.closebox {
  background: none;
  color: white;
  font-size: 50px;
  padding: 0;
  margin: 0.4em;
  width: 50px;
  height: 50px;
  line-height: 50px;
}

@media (hover: hover) {
  .other-speakers li button:hover {
    opacity: .7;
  }
  .other-speakers li button.empty:hover {
    opacity: 1;
  }
}

@media screen and (-ms-high-contrast: active), (-ms-high-contrast: none) {
  .other-speakers li button:hover {
    opacity: .7;
  }
  .other-speakers li button.empty:hover {
    opacity: 1;
  }
}

@media screen and (max-width: 1024px) {
  #speakers .content {
    padding: 2em;
  }
}

@media screen and (max-width: 768px) {
  .other-speakers > li {
    width: 30%;
    margin: 2% 1.66667%;
  }
}

@media screen and (max-width: 767px) {
  #speakers .content {
    display: block;
  }
  #speakers .content figure {
    width: 100%;
  }
  .main-speaker-img {
    margin-bottom: 1em;
  }
  .main-speaker-img img {
    width: 50%
  }
  .main-speaker {
    width: 100%;
  }
}

@media screen and (max-width: 640px) {
  #speakers .content {
    padding: 1.5em 0;
  }
}

@media screen and (max-width: 480px) {
  .main-speaker article {
    padding: 0 2.5%;
  }
  .main-speaker-img img {
    width: 60%;
  }
  .other-speakers > li {
    width: 45%;
    margin: 5% 2.5%;
  }
  .other-speakers {
    margin-top: 0;
  }
  .other-speakers img {
    width: 100%;
    border-width: 3px;
  }
}

</style>
