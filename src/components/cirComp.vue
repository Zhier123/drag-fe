<template>
  <div class="Box" 
  @click="clickHandler"
>
    <img width="120" height="80" alt="对应图片" :src="require(`../assets/${this.type}.png`)"/>
    <h4>{{this.type}}</h4>
  </div>
</template>
<script>
export default {
  props:{
    type:String,
  },
  //暂时不计单位
  data(){
    return{
      value:100   //默认值后面可以修改
    }
  },
  methods:{
    clickHandler(){
      this.$emit('genComponent',this.type)
    },
    
  }
}
</script>
<style scoped>
  .Box{
    text-align:center;
    transition-duration: 0.5s;
    padding:5px;
    color:white
  }
  .Box:hover{
    background: rgba(216, 191, 216, 0.479);
  }
</style>