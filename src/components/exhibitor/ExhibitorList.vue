<template>
  <li
    :class="showDetails ? 'exhibitor-list active' : 'exhibitor-list'"
    @mouseover="handleMouseover"
    @mouseleave="handleMouseleave"
    @click="handleClick"
  >
    <div>
      <article>
        <h3><span>{{ exhibitor.title }}</span></h3>
        <p>{{ exhibitor.description }}</p>
      </article>
    </div>
  </li>
</template>

<script>
export default {
  props: {
    exhibitor: {
      type: Object,
      required: true
    },
    isMobile: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      showDetails: false
    }
  },
  methods: {
    handleMouseover() {
      if(!this.isMobile) this.showDetails = true;
    },
    handleMouseleave() {
      if(!this.isMobile) this.showDetails = false;
    },
    handleClick() {
      if(this.isMobile) this.showDetails = !this.showDetails;
    }
  }
}
</script>

<style>
.exhibitor-list {
  position: relative;
  width: 30%;
  padding-bottom: 35%;
  margin: 1em 0 0;
  background: #f09819;
  color: white;
  cursor: pointer;
}
.exhibitor-list div {
  position: absolute;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
  padding: 1em;
}
.list-background {
  background-size: cover;
  background-position: center;
  opacity: .25;
  transition: .5s;
}
.exhibitor-list div article {
  border: solid 2px white;
  height: 100%;
  padding: 0 0.5em;
  display: flex;
  justify-content: center;
  align-items: stretch;
  flex-wrap: wrap;
  overflow: hidden;
}
.exhibitor-list h3 {
  display: flex;
  align-items: center;
  min-height: 100%;
  margin-bottom: 0.6em;
  -webkit-transition: all 500ms cubic-bezier(0.250, 0.460, 0.450, 0.940);
  -moz-transition: all 500ms cubic-bezier(0.250, 0.460, 0.450, 0.940);
  -o-transition: all 500ms cubic-bezier(0.250, 0.460, 0.450, 0.940);
  transition: all 500ms cubic-bezier(0.250, 0.460, 0.450, 0.940);
}
.exhibitor-list h3 span {
  display: inline-block;
  padding: 0.5em 0;
  border-bottom: solid 2px white;
  text-shadow: 2px 2px 5px rgba(0, 0, 0, .4);
}
.exhibitor-list div p {
  margin-top: 0;
  line-height: initial;
}

.exhibitor-list.active h3 {
  min-height: 5%;
}
.exhibitor-list.active .list-background {
  opacity: .05;
}

@media screen and (max-width: 1024px) {
  .exhibitor-list {
    width: 32%;
    padding-bottom: 45%;
  }
}

@media screen and (max-width: 768px) {
  .exhibitor-list {
    width: 45%;
    padding-bottom: 65%;
  }
  .exhibitor-list div {
    padding: 0.6em;
  }
}

@media screen and (max-width: 640px) {
  .exhibitor-list {
    margin: 1em 0;
    width: 100%;
    padding-bottom: 100%;
  }
}

</style>