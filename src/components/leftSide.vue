<template>
  <div class="con">
    <cirComp 
    v-for="item in compList" 
    :key="item.Type"
    :type="item.Type"
    @genComponent="genComponent"
    >
    </cirComp>
  </div>  
</template>
<script>
import cirComp from "./cirComp.vue"
export default {
  components:{
    cirComp
  },
  data(){
    return{
      compList:[
        {
          Type:"Resistor",
        },
        {
          Type:"Voltage"
        }
      ]
    }
  },
  methods:{
    genComponent(type){ 
      this.$emit("genComponent",type);
    }
  }
}
</script>
<style scoped>
  .con{
      flex-shrink: 0;
    background-color: rgb(5, 5, 5);
    height:100%;
    width:140px;
  }
</style>