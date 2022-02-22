<template>
  <div class="container" >
    <window-group :metadata="metadata">
      <template v-slot:window1>
        window 1
      </template>
      <template v-slot:window2>
        Window 2
      </template>
    </window-group>
  </div>
</template>

<script>
import windowGroup from './components/window/windowGroup.vue'
  export default {
    components: {
      windowGroup
    },
    data(){
      return {
        metadata : [
          {
            "title": "Window 1",
            "name": "window1",
          },
          {
            "title": "Window 2",
            "name": "window2",
          }
        ]
      }
    }
  }
</script>
