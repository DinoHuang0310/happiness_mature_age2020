<template>
  <div id="information" class="area">
    <div class="wrapper">
      <div class="title">
        <h2><span>活動資</span>訊</h2>
      </div>
      <ul>
        <li data-title="日期">2020年10月29日(四) 9:30-16:30</li>
        <li data-title="地點">格萊天漾大飯店15樓天闊廳<br>(台北市萬華區艋舺大道101號)</li>
      </ul>
      <div class="information-box">
        <iframe
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3615.019239271926!2d121.49919595124739!3d25.03342114438854!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3442a9af74dc5381%3A0x321fb4825e85fb39!2z5qC86JCK5aSp5ry-5aSn6aOv5bqXIEdyZWF0IFNreXZpZXc!5e0!3m2!1szh-TW!2stw!4v1600415353981!5m2!1szh-TW!2stw"
          frameborder="0"
          aria-hidden="false"
          tabindex="0"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
}
</script>

<style>
#information {
  text-align: center;
}
#information ul {
  display: inline-block;
  text-align: left;
}
#information ul li {
  position: relative;
  letter-spacing: 0.2em;
}
#information ul li::before {
  content: attr(data-title)": ";
  position: absolute;
  left: -0.5em;
  transform: translate(-100%, 0);
}
.information-box {
  position: relative;
  padding-bottom: 35%;
  margin-top: 2em;
}
.information-box iframe {
  position: absolute;
  border: none;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
}

@media screen and (max-width: 480px) {
  #information ul {
    display: block;
  }
  #information ul li {
    margin-top: 0.5em;
  }
  #information ul li::before {
    position: relative;
    display: block;
    left: 0;
    font-weight: bold;
    transform: translate(0, 0);
  }
  .information-box {
    padding-bottom: 60%;
  }
}

</style>
