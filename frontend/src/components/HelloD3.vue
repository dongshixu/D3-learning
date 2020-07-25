<!--
 * @Descripttion: 
 * @version: 
 * @Author: xds
 * @Date: 2020-07-19 17:03:13
 * @LastEditors: xds
 * @LastEditTime: 2020-07-25 21:16:48
--> 
<template>
  <div id="container">
    <div id="container-header">
      <div id="container-header-category"></div>
      <div id="container-header-subtool"></div>
    </div>
    <div id="container-content">
      <div id="draw-siderbar">
        <button @click="drawRectangle">画图</button>
      </div>
      <div id="draw-area">
        <div id="work-space">
          <div id="page">
            <svg id="svg-canvas" width="100%" height="100%" style="position: absolute; top: 0; left: 0;">
            <rect fill="#ffffff" fill-opacity="0" width="100%" height="100%"></rect>
          </svg>
          </div>
          <svg id="svg-canvas-selected" width="100%" height="100%" style="position: absolute; top: 0; left: 0; pointer-events: none">
            <rect fill="#ffffff" fill-opacity="0" width="100%" height="100%"></rect>
          </svg>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import * as d3 from 'd3'

export default {
  name: 'workspace',
  data() {
    return{
      globalCanvas: '',
      globalEleSize: 1,
      globalCanvasG: '',
      currentGId: '',
      globalCanvasSelected: '',
      globalCanvasGSelected: '',
      testObject: {}
    }
  },
  computed:{

  },
  watch:{

  },
  created() {
    
  },
  mounted() {
    this.getRootSvg()
    // this.drawRectangle()
  },
  destroyed() {

  },
  methods: {
    getRootSvg() {
      this.globalCanvas = d3.select("#svg-canvas")
      this.globalCanvasG = this.globalCanvas.append('g')
      this.globalCanvasSelected = d3.select("#svg-canvas-selected")
      this.globalCanvasGSelected = this.globalCanvasSelected.append('g')
    },
    drawRectangle() {
      var vm = this
      var currentCoordinate = []
      this.globalCanvas
      .on('mousedown', function(){
        const initXY = d3.mouse(this)
        const gId = "editor-" + (vm.globalCanvas.selectAll('path').size())
        vm.currentGId = gId
        const currentCanvas = vm.globalCanvasG.append('g')
                                              .attr("id", gId)
                                              .on('mousedown', function() {
                                                  console.log(vm.testObject[d3.select(this).attr("id")])
                                              })
                                              .call(d3.drag()
                                                      .on("drag", function(){
                                                        console.log(d3.event)
                                                        console.log(this)
                                                      })
                                              )

        vm.globalCanvas.on('mousemove', ()=>{
          currentCoordinate = [[initXY[0], initXY[1], d3.mouse(this)[0], d3.mouse(this)[1]]]
          vm.draw(currentCanvas, currentCoordinate, vm.rectangleRoundPath, 'red')
        })
      })
      .on('mouseup', ()=>{
        this.testObject[this.currentGId] = currentCoordinate
        d3.select('#' + this.currentGId).select('path').attr('fill', '#CFE2F3').attr('fill-opacity', 1)
        // console.log(this.testObject)
        // this.drawSelected(currentCoordinate)
        this.globalCanvas.on('mousemove', null)
        this.globalCanvas.on('mousedown', null)
      })
    },
    draw(el, arr, drawType, strokeColor) {
      const rectUpdate = el.selectAll('path').data(arr)
      const rectEnter = rectUpdate.enter()
      const rectExit = rectUpdate.exit()

      rectUpdate
      .attr("d", (d)=>{
        return drawType(d)
      })
      .attr('stroke', strokeColor)
      .attr('fill-opacity', 0)
      
      rectEnter
      .append("path")
      .attr("d", (d)=>{
        return drawType(d)
      })
      .attr('stroke', strokeColor)
      .attr('fill-opacity', 0)

      rectExit.remove()
    },

    drawSelected(coordinate){
      const gContainer = this.globalCanvasGSelected.append('g')
                                                   .attr("pointer-events", "visiblePainted")
      const subGContainer1 = gContainer.append('g')
                                       .attr("pointer-events", "visiblePainted")
      // const subGContainer2 = gContainer.append('g')
      //                                  .attr("pointer-events", "visiblePainted")
      // const subGContainer3 = gContainer.append('g')
      //                                  .attr("pointer-events", "visiblePainted")
      this.draw(subGContainer1, coordinate, this.rectangleRoundPath, 'rgb(26, 115, 232)')

    },

    rectangleRoundPath(arr) {
       return "M" + arr[0] + "," + arr[1]
       + "L" + arr[2] + "," + arr[1] + "," + arr[2] + "," + arr[3] + "," + arr[0] + "," + arr[3]
       + "z"
    },


  }
}
</script>

<style lang="less" scoped>
  #container{
    height: 100%;
    background-color: white;
    text-align: center;
    color: #2c3e50;
    z-index: 10;
    display: flex;
    flex-direction: column;
    #container-header{
      height: 62px;
      background-color: #535353;
      z-index: 20;
    }
    #container-content{
      height: 661px;
      background-color: #fff;
      display: flex;
      flex-direction: row;
      z-index: 20;
      #draw-siderbar{
        background-color: #535353;
        width: 42px;
        height: 100%;
      }
      #draw-area{
        background-color: #F8F9FA;
        height: 100%;
        width: 1494px;
        position: relative;
        #work-space{
          height: 100%;
          #page{
            height: 100%;
          }
        }
      }
    }
  }
</style>
