<!--
 * @Descripttion: 
 * @version: 
 * @Author: xds
 * @Date: 2020-07-19 16:37:59
 * @LastEditors: xds
 * @LastEditTime: 2020-07-25 18:11:27
--> 
<template>
  <div id="app">
    <HelloD3/>
  </div>
</template>

<script>
import HelloD3 from './components/HelloD3.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld
    HelloD3
  }
}
</script>

<style lang="scss" scoped>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    /* margin-top: 60px; */
    height: 100%;
    z-index: 1;
  }
</style>
<style>
  body {
    height: 100%;
    -moz-osx-font-smoothing: grayscale;
    -webkit-font-smoothing: antialiased;
    text-rendering: optimizeLegibility;
    font-family: Helvetica Neue, Helvetica, PingFang SC, Hiragino Sans GB, Microsoft YaHei, Arial, sans-serif;
    margin: 0px;
  }

  html {
    height: 100%;
    box-sizing: border-box;
  }

</style>
