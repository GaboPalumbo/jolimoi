<template>
  <div id="app">
    <Header msg="This is a page for<br>beauty product search" color="#55D7FF" img="beauty-products.jpg"
      alt="search beauty product image" />
    <SearchProducts color="#DB0992" msg="Search by product or brand name" :errors="errors" :limit="3000"/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import SearchProducts from './components/SearchProducts.vue'
import BaseView from './components/BaseView.vue'

export default {
  name: 'app',
  components: {
    Header,
    SearchProducts,
    BaseView
  },
  data() {
    return {
      errors: ["sorry no results founded!",
        "too many products are matched these criteria, please make a more specific research",
        "sorry we couldn't complete your request"
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
  display: table;
  background-color: rgb(219, 9, 146);
  width: 100%;
  max-width: 800px;
  height: 100%;
  left: 50%;
  /* margin: auto; */
  position: absolute;
  transform: translateX(-50%);
}

body {
  display: block;
  margin: 0px;
}
</style>
