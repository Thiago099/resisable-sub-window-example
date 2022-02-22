<template>
    <div ref="window" class="window"  @mousedown="$emit('focus')">
      <div ref='header' class="header">
        <div class="title"><img class = "icon" src="./assets/icon.svg" >{{ title }}</div>
        <div @mousedown="preventDrag">
          <div class="nav-button close-button" @click="$emit('close')"><div>×</div></div>
          <!-- <div class="nav-button maximize-button"><div>🗗</div></div>
          <div class="nav-button minus-button" ><div>-</div></div> -->
        </div>
      </div>
      <div class="content">
        <slot name="content">aaa</slot>
      </div>
    </div>
</template>
<script>
import dragElement from './plugins/drag.js'
import resizeElement from './plugins/resize.js'
  export default {
    props: {
      title: {
        type: String,
        default: 'title'
      },
    },
    mounted(){
      dragElement(this.$refs.window, this.$refs.header);
      resizeElement(this.$refs.window);
    },
    methods:{
      preventDrag(event){
        event.cancelBubble = true
        event.preventDefault()
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
  overflow: hidden;
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
  padding: 10px;
}
.header > .title{
  margin-top: -8px;
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
  margin-right: 3px;
}
.footer {
   position: fixed;
   left: 0;
   bottom: 0;
   width: 100%;
   text-align: center;
}
</style>