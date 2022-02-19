<template>
  <div class="container">
    <div ref="window" class="window" v-show="display">
      <div ref='header' class="header">
        <div class="title"><img class = "icon" src="./assets/icon.svg" alt="vue logo"> Drag here to move</div>
        <div class="close-button" @click="display = false"><div>×</div></div>
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
        display: true
      }
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
.close-button{
  cursor: pointer;
  float: right;
  font-size: 1.6em;
  width: 50px;
  height: 30px;
  text-align: center;
  overflow: hidden;
  transition: background-color .2s;
  border-radius: 0 5px 0 0;
  position: absolute; top: 0px; right: 0px;
}
.close-button:hover{
  background-color: red;
}
.close-button > div{
  margin-top: -7px;
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
    border:1px solid #b8b8b8;
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
