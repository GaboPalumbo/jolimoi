<template>
  <div class="baseview" v-bind:style="getColor(color)">
    <div class="section">
      <h1 v-html="msg"></h1>
    </div>
    <div class="section"><img v-bind:src="getImg(img)" :alt="alt"></div>
  </div>
</template>
<script>
import BaseView from './BaseView.vue';
export default {
  name: 'Header',
  extends: BaseView
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  /* font-size: 12px; */
  font-size: 2.2vw;
  font-weight: 700;
  text-align: center;
  margin: auto;
  letter-spacing: -0.2px;
}

.section {
  padding: 0;
  display: table-cell;
  margin: 0px;
  width: 50%;
  position: relative;
  vertical-align: middle;
}

.section>img {
  width: 100%;
  margin: 0;
  padding: 0;
  display: block;
  height: auto;
}

@media screen and (min-width: 1024px) {
  h1 {
    font-size: 20px;
  }
}

@media only screen and (max-width: 600px) {

  /* For mobile phones: */
  .section {
    display: block;
    width: 100%;
    height: 34vh;
    overflow: hidden;
  }

  .section>img {
    height: auto;
    margin: auto;
    padding: 0;
    display: block;
    width: 100%;
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
  }

  h1 {
    font-size: 18px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
}

@media only screen and (max-width: 360px) {
  .section>img {
    height: 100%;
    width: auto;
  }
}
</style>
