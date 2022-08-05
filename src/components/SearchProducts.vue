<template>
  <div class="baseview" v-bind:style="getColor(color)">
    <form id="search" v-on:submit.prevent="checkForm">
      <input type="search" name="field" id="field" v-model="field" :placeholder="msg">
      <input type="submit" value="Search" :disabled="(this.field.length < 2)">
      <p v-if="errorsList.length">
      <ul>
        <li v-for="error in errorsList" :key="error">{{ error }}</li>
      </ul>
      </p>
      <p v-if="!errors.length && products.length">
      <ul>
        <li v-for="product in products" :key="product.id"><b>{{ product.brand }}</b> - <span>{{ product.name }}</span>
        </li>
      </ul>
      </p>
    </form>
  </div>
</template>
<script>

import BaseView from './BaseView.vue';
import axios from 'axios';

export default {
  name: 'SearchProducts',
  extends: BaseView,
  data: function () {
    return {
      errors: [],
      errorsList: [],
      limit: 0,
      products: [],
      isDisabled: false,
      field: ''
    };
  },
  methods: {
    checkForm() {
      let url = "https://thawing-scrubland-03171.herokuapp.com/https://skincare-api.herokuapp.com/products?q=";
      url += this.field;
      url += "&limit=25&page=1";
      axios
        .get(url)
        .then(response => {
          this.errorsList = [];
          this.products = [];
          if (!response) {
            this.errorsList.push(this.errors[0])
            return;
          }

          if (response.data.length > this.limit) {
            this.errorsList.push(this.errors[1])
            return;
          }

          this.products = response.data;
        })
        .catch(error => {console.log(error); this.errorsList.push(this.errors[2])})
    }
  }
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input {
  font-size: 12px;
  padding: 6px;
  border: 1px solid grey;
  border-radius: 5px;
  margin-right: 10px;
}

input[type="search"] {
  width: 300px;
}

input[type="submit"] {
  background-color: #55D7FF;
  padding-left: 20px;
  padding-right: 20px;
  margin-left: 10px;
  margin-right: 0px;
  cursor: pointer;
  font-weight: bold;
}

input:not(:disabled)[type="submit"]:hover {
  border: 1px solid white;
}

form {
  width: 50%;
  min-width: 640px;
  margin: auto;
  margin-top: 40px;
}

ul {
  text-align: left;
  color: white;
}

li:first-letter {
  text-transform: uppercase;
}

span:first-letter {
  text-transform: uppercase;
}
</style>
