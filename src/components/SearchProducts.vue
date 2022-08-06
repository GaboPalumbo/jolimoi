<template>
  <div class="baseview" v-bind:style="getColor(color)">
    <form id="search" v-on:submit.prevent="checkForm">
      <input type="search" name="field" id="field" v-model="field" :placeholder="msg">
      <input type="submit" value="Search" :disabled="(this.field.trim().length < 2) || isDisabled">
      <p v-if="errorsList.length">
      <ul class="errors">
        <li v-for="error in errorsList" :key="error">{{ error }}</li>
      </ul>
      </p>
      <p v-if="!errorsList.length && products.length">
      <ul class="products" >
        <li v-for="product in products" :key="product.id"><b>{{ product.brand }}</b> - <span>{{ product.name }}</span>
        </li>
      </ul>
      </p>
      <div v-if="isDisabled" class="lds-dual-ring"></div>
    </form>
  </div>
</template>
<script>

import BaseView from './BaseView.vue';
import axios from 'axios';

export default {
  name: 'SearchProducts',
  extends: BaseView,
  props: {
    errors: Array,
    limit: Number,
  },
  data: function () {
    return {
      errorsList: [],
      products: [],
      isDisabled: false,
      field: ''
    };
  },
  methods: {
    checkForm() {
      let url = "https://thawing-scrubland-03171.herokuapp.com/https://skincare-api.herokuapp.com/products?q=";

      let keywords = this.field.split("");

      keywords.forEach(element => {
        url += element;
      });

      this.isDisabled = true;
      axios
        .get(url)
        .then(response => {
          this.isDisabled = false;
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

          response.data.forEach(element => {
            let product ={
              id:element.id,
              brand:element.brand,
              name:element.name
            }
            this.products.push(product);
          });
          console.log(response.data);
          //this.products = response.data;
        })
        .catch(error => { this.isDisabled = false; console.log(error); this.errorsList.push(this.errors[2]) })
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

.errors {
  color: white;
  font-size: 12px;
  font-style: italic;
  width: 80%;
  margin: auto;
  text-align: center;
  padding-inline-start: 0px;
  margin-block-start: 0px;
  list-style-type: none;
}
.products{
    width: 450px;
    margin: auto;
    font-size: 12px;
    line-height: 15px;
    padding-inline-start: 0px;
}

li:first-letter {
  text-transform: uppercase;
}

span:first-letter {
  text-transform: uppercase;
}

.lds-dual-ring {
  width: 50px;
  height: 50px;
  margin: auto;
  margin-top: 20px;

}

.lds-dual-ring:after {
  content: " ";
  display: block;
  width: 34px;
  height: 34px;
  margin: 8px;
  border-radius: 50%;
  border: 6px solid #fff;
  border-color: #fff transparent #fff transparent;
  animation: lds-dual-ring 1.2s linear infinite;
}

@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}


@media only screen and (max-width: 600px) {

  form {
    margin-top: 15px;
  }

  input {
    margin-right: 5px;
  }

  input[type="search"] {
    width: 270px;
  }

  input[type="submit"] {
    margin-left: 5px;
    margin-right: 0px;
  }

  .products{
    width: 80%;
  }
}
</style>
