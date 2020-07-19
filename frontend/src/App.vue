<!--
 * @Descripttion: 
 * @version: 
 * @Author: xds
 * @Date: 2020-07-19 16:37:59
 * @LastEditors: xds
 * @LastEditTime: 2020-07-19 17:10:16
--> 
<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <HelloD3/>

  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import HelloD3 from './components/HelloD3.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld
    HelloD3
  }
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
