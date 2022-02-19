<template>
  <div class="container">
    <div ref="window" class="window">
      <div ref='header' class="header">
        <div class="title"><img class = "icon" src="./assets/icon.svg" alt="vue logo"> Drag here to move</div>
        <div class="close-button"><div>×</div></div>
      </div>
      <div class="content">
        
        <p>Drag on the corenersto resize the window</p>
      </div>
    </div>
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
  margin-right: 5px;
  width: 50px;
  height: 30px;
  text-align: center;
  overflow: hidden;
  margin-top: -27px;
  margin-right: -11px;
  transition: background-color .2s;
  border-radius: 0 5px 0 0;
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
</style>
