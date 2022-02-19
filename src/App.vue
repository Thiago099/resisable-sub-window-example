<template>
  <div class="container">
    <div ref="window" class="window">
      <div ref='header' class="header">Click here to move<i class="fa-solid fa-xmark"></i><i class="close fa fa-times no-print"></i></div>
      <div class="content">
        
        <p>Drag on the coreners</p>
        <p>to resize</p>
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

}

.content{
  overflow: auto;
  width: 100%;
  height: calc(100% - 45px); 
}

.header {
  padding: 10px;
  z-index: 10;
  background-color: #2196F3;
  color: #fff;
  height: 45px;
}
.close{
  cursor: pointer;
  float: right;
  font-size: 1.5em;
}
</style>
