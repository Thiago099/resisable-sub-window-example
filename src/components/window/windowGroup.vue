<template>
  <div class="container">
    <window 
      v-for="(item, index) in meta"
      :key="index"
      v-show="item.visible"
      @close="item.visible = 0" 
      @focus="focus(item)"
      :title="item.title"
      :style="`z-index: ${item.zindex}`"
    >
      <template v-slot:content>
          <slot :name="item.name"></slot>
      </template>
    </window>
    <div class="footer" style="z-index: 10;">
      <a v-for="(item, index) in metaVisible" 
      :key="item.name" 
      @click="item.visible = 1"
      style="cursor: pointer;"
      >
        {{ item.title }}
        <a v-if="index != metaVisible.length-1"> | </a>
      </a>
      </div>
  </div>
</template>

<script>
import window from './window.vue'
export default {
  components: {
    window
  },
  props:{
    metadata: {
      type: Array,
    },
  },
  data(){
    return{
      display: true,
      meta:[]
    }
  },
  mounted(){
      this.meta = this.metadata
      this.meta.forEach(window => {
        window.zindex = 1
        window.visible = 1
      })
  },
  methods:{
    focus(item)
    {
      for(let i = 0; i < this.meta.length; i++)
      {
        this.meta[i].zindex = 1
      }
      item.zindex = 2
    },

  },
  computed: {
    metaVisible(){
      return this.meta.filter(window => !window.visible)
    }
  }
}
</script>
<style scoped>
.footer {
   position: fixed;
   left: 0;
   bottom: 0;
   width: 100%;
   text-align: center;
}
</style>
