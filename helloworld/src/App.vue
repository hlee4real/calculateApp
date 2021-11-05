<template>
  <div id="app">
    
    <HelloWorld msg="Welcome to Your Vue.js App"/>

    <div class="mt-2"><h2>Welcome to calculate application </h2></div>
    
    <div>
      <h2 class="mt-5">calculate</h2>
      <b-form-input type="number" v-model="a" placeholder="Enter A" class="mt-2" id="num1"></b-form-input>
      <b-form-input type="number" v-model="b" placeholder="Enter B" class="mt-3" id="num2"></b-form-input>
    </div>
    <div class="mt-2"> 
      <div class="mt-2"><b-button @click="calculate()">Addition {{sum}}</b-button></div>
      <div class="mt-2"><b-button @click="calculate2()" variant="danger">Subtraction {{sub}}</b-button></div>
      <div class="mt-2"><b-button @click="calculate3()" variant="success">Multiplication {{mul}}</b-button></div>
      <div class="mt-2"><b-button @click="calculate4()" variant="outline-primary">Division {{div}}</b-button></div>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Vue from 'vue'
import { BootstrapVue, IconsPlugin } from 'bootstrap-vue'

// Import Bootstrap an BootstrapVue CSS files (order is important)
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'
// Make BootstrapVue available throughout your project
Vue.use(BootstrapVue)
// Optionally install the BootstrapVue icon components plugin
Vue.use(IconsPlugin)
export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data(){
    return {
      sum:null,
      sub:null,
      mul:null,
      div:null,
      a: 0,
      b: 0
    }
  },
  methods:{
    calculate(){
      let params = {
        a: this.a,
        b: this.b
      };
      let query = Object.keys(params).map(k=> encodeURIComponent(k) + '=' +encodeURIComponent(params[k])).join('&')
      let targetUrl = 'http://localhost:3334/calADD?'+query;

      fetch(targetUrl).then(res =>
        res.json()
      ).then(sum =>{
        console.log(sum);
        return this.sum = sum;
      })
    },
    calculate2(){
      let params = {
        a: this.a,
        b: this.b
      };
      let query = Object.keys(params).map(k=> encodeURIComponent(k) + '=' +encodeURIComponent(params[k])).join('&')
      let targetUrl = 'http://localhost:3334/calSUB?'+query;

      fetch(targetUrl).then(res =>
        res.json()
      ).then(sub =>{
        console.log(sub);
        return this.sub = sub;
      })
    },
    calculate3(){
      let params = {
        a: this.a,
        b: this.b
      };
      let query = Object.keys(params).map(k=> encodeURIComponent(k) + '=' +encodeURIComponent(params[k])).join('&')
      let targetUrl = 'http://localhost:3334/calMUL?'+query;

      fetch(targetUrl).then(res =>
        res.json()
      ).then(mul =>{
        console.log(mul);
        return this.mul = mul;
      })
    },
    calculate4(){
      let params = {
        a: this.a,
        b: this.b
      };
      if(this.b == 0){
        alert('Can not divide any number by 0');
      }else{
        let query = Object.keys(params).map(k=> encodeURIComponent(k) + '=' +encodeURIComponent(params[k])).join('&')
        let targetUrl = 'http://localhost:3334/calDIV?'+query;
      
        fetch(targetUrl).then(res =>
          res.json()
        ).then(div =>{
          console.log(div);
          return this.div = div;
        })
      }
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
