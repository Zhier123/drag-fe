<template>
  <div class="con">
    <p>type:{{type}}</p>
    <p>name:{{name}}</p>
    <p>value:{{value}}</p>
    <input placeholder="ChangeValue"/>
    <button @click="ChangeValue">修改</button>
    <p>port1:{{ports.port1}}</p>
    <p>port2:{{ports.port2}}</p>
  </div>
</template>
<script>
export default {
  props:{
    type:String,
    value:Number,
    name:String,
    ports:Object
  },
  data(){
    return{
      modValue:this.value
    }
  },
  methods:{
    ChangeValue(){
      alert("change")   
    }
  }
}
</script>
<style scope>
  .con{
    height: 100%;
    background: tomato;
  }
</style>