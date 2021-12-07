<template>
  <div id="app">
    <leftSide
    @genComponent="genComponent"></leftSide>
    <MainContainer ref="canvas"></MainContainer>
  </div>
</template>
<script>
import leftSide from './components/leftSide.vue'

import MainContainer from './components/MainContainer.vue'
export default {
  components:{
    leftSide,
    MainContainer,
    
  },
  data(){
    return{
    }
  },
  methods:{
    genComponent(type){
      console.log(type);
       this.$refs.canvas.genComponent(type);//图像添加
    }
  }
}
</script>
<style>
*{
  box-sizing: border-box;
  padding: 0;
  margin:0;
}
body,html{
  margin:0;
  padding:0;
  height: 100%;
  width: 100%;
}
#app{
  width: 100%;
  height:100%;
  background-color: thistle;
  display: flex;

}
</style>
