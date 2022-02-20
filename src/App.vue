<template>
  <div class="container">
    <div ref="window" class="window" v-show="display">
      <div ref='header' class="header" @mousedown="dragResize">
        <div class="title"><img class = "icon" src="./assets/icon.svg" alt="vue logo"> Drag here to move</div>
        <div @mousedown="preventDrag">
          <div class="nav-button close-button" @click="display = false"><div>×</div></div>
          <div class="nav-button maximize-button" @click="fullScreen()"><div>🗗</div></div>
          <div class="nav-button minus-button" ><div>-</div></div>
        </div>
      </div>
      <div class="content">
        <p>Drag on the coreners to resize the window</p>
      </div>
    </div>
    <div v-show="!display" class="pop-up" @click="display = true">re-open</div>
  </div>
</template>

<script>
  import dragElement from './plugins/drag.js'
  import resizeElement from './plugins/resize.js'

  // import {onresize, resizeX, resizeY} from './resize.js'
  export default {
    mounted(){
      dragElement(this.$refs.window, this.$refs.header);
      resizeElement(this.$refs.window);
    },
    data(){
      return{
        display: true,
        full:false,
        prevwidth:0,
        prevheight:0,
        preveleft:0,
        prevtop:0
      }
    },
    methods:{
      preventDrag(event){
        event.cancelBubble = true
        event.preventDefault()
      },
      fullScreen()
      {
        this.full = !this.full
        if(this.full)
        {
          this.prevwidth = this.$refs.window.style.width
          this.prevheight = this.$refs.window.style.height
          this.preveleft = this.$refs.window.style.left
          this.prevtop = this.$refs.window.style.top
          this.$refs.window.style.width = '99%'
          this.$refs.window.style.height = '99%'
          this.$refs.window.style.top = '0px'
          this.$refs.window.style.left = '0px'
        }
        else
        {
          this.$refs.window.style.width = this.prevwidth
          this.$refs.window.style.height = this.prevheight
          this.$refs.window.style.top = this.prevtop
          this.$refs.window.style.left = this.preveleft
        }
      },
    }
  }
</script>
<style scoped>
.window {
  position: absolute;
  z-index: 9;
  background-color: #f1f1f1;
  border: 1px solid #d3d3d3;
  left: calc(50% - 800px / 2);
  top: calc(50% - 500px / 2);
  width: 800px;
  height: 500px;
  border-radius: 5px;
}
.content{
  margin-top: 0px;
  overflow: auto;
  width: 100%;
  height: calc(100% - 45px); 
}
.header > .title{
  margin-top: -9px;
}
.header {
  overflow: hidden;

  border-radius: 5px 5px 0 0;
  padding: 10px;
  z-index: 10;
  background-color: #2196F3;
  border:1px solid #2196F3;
  color: #fff;
  height: 30px;
  
}
.nav-button{
  cursor: pointer;
  float: right;
  font-size: 1.6em;
  width: 30px;
  height: 30px;
  text-align: center;
  /* overflow: hidden; */
  transition: background-color .2s;
  background-color: #2196F3;
  position: absolute; top: 0px; right: 0px;
}
.nav-button:hover{
    background-color: #1d7cca;
}
.close-button{
    border-radius: 0 5px 0 0;
}
.close-button > div{
  margin-top: -7px;
}
.close-button:hover{
  background-color: red;
}
.maximize-button{
  font-size: 14pt;
  margin-right: 30px;
}
.maximize-button > div{
  margin-top: -1px;
}
.minus-button{
  font-size: 30pt;
  margin-right: 60px;
}
.minus-button > div{
  margin-top: -20px;
}

.icon{
  width: 20px;
  margin-top: -3px;
  margin-left: -3px;
}
.footer {
   position: fixed;
   left: 0;
   bottom: 0;
   width: 100%;
   text-align: center;
}
.pop-up {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translateX(-50%) translateY(-50%);
    font-size: 3em;
    padding: 10px 40px 20px 40px;
    border-radius: 10px;
    transition: background-color .2s;
    cursor: pointer;
  background-color: #f1f1f1;
  border: 1px solid #d3d3d3;
}
.pop-up:hover{
  background-color: green;
  color:white;
}
.footer {
   position: fixed;
   left: 0;
   bottom: 0;
   width: 100%;
   text-align: center;
}
</style>
