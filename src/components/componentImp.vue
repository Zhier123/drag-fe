<template>
  <div class="imp" 
  draggable="true"
  @dragstart="dragstart"
  @ondrag="ondrag"
  @dragend="dragend"
  @click="clickHandler"
    @contextmenu="showMenu"
     v-bind:class="{ active:isactive}"
  >
    <div>{{name}} </div>
    <div class="comp">
    <Node class="port"
    @nodeLink="nodeLink"
    ></Node>
    <img width="30" height="30" alt="示例图片" :src="require(`../assets/${this.type}_remix.png`)"/>
    <Node class="port"
    @nodeLink="nodeLink"></Node>
    </div>
    <div>{{value}}</div>
  </div> 
</template>
<script>
import Node from './Node.vue'
export default {
  components:{
    Node
  },
  props:{
    index:Number,
    type:String,
    value:Number,
    name:String,
    current:Number
  },
  data(){
    return{
      offsetX:0,
      offsetY:0
    }
  },
  computed:{
    isactive(){
      return this.index ==this.current
    }
  },
  methods:{
    dragstart(ev){
      this.$emit("chosen",this.index);
      // console.log(ev)
      // console.log("start")
      this.offsetX = ev.offsetX;
      this.offsetY = ev.offsetY;
    },
    ondrag(ev){
      console.log(ev)
      // console.log("ondrag")
    },
    clickHandler(){
      this.$emit("chosen",this.index)
    },
     dragend(ev){
      // console.log(ev)
      // console.log("dragend")
      const imp  = this.$el
      imp.style.position = "absolute"
      // console.log(imp.style)
      imp.style.left =10*Math.round((ev.clientX-140-this.offsetX)/10)+"px";
      imp.style.top =10*Math.round((ev.clientY-this.offsetY)/10)+"px";
    },
    showMenu(event){
     const  data={
        index:this.index,
        x:event.clientX,
        y:event.clientY
      }
       event.preventDefault();
      // console.log("子组件")
      this.$emit("chosen",this.index);
      this.$emit("showMenu",data);
    },
    nodeLink(data){
      console.log("通过子组件上传",data);
      this.$emit("nodeLink",data);
    }
  }
}
</script>
<style scoped>
  .imp{
    box-sizing:border-box;
    width: 50px;
    height: 90px; 
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  .active{
    border: 2px solid rgb(19, 132, 224);
  }
  .comp{
    display: flex;
    align-items: center;
  }
  .port2{
    transform: rotate(180deg);
  }
  .port{
    cursor: pointer;;
  }
</style>