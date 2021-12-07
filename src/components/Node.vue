<template>
    <img width="10" height="10" :src="require(`../assets/line.png`)" @click="NodeclickHandler"/>
</template>
<script>
import _global from './Global.vue'
export default {
  data(){
    return{
    }
  },
  methods:{
    NodeclickHandler(ev){//drawing 表示当前的画线状态
      ev.cancelBubble=true;
      console.log("port clicked");
      const data={
        X:_global.px2pixiv(ev.clientX-140),
        Y:_global.px2pixiv(ev.clientY)
      }
      this.$emit("nodeLink",data)
    }
  }
}
</script>
<style scoped>
</style>