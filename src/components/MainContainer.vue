<template>
  <div style="display:flex;">
  <div id="canvas"
   @ondrop="drophandler" 
   @ondragover="dragover_handler"
   @click="clickHandler"
   >
   <vue-context-menu :contextMenuData="contextMenuData" @savedata="savedata" @newdata="newdata"></vue-context-menu>
    <component-imp v-for="item in componentList" :key = item.name
      :type = item.type
      :value = item.value
      :name = item.name
      :index= item.index
      :current ="current"
       @showMenu="showMenu"
       @chosen="chosen"
       @nodeLink="nodeLink"
      > 
    </component-imp>
    <!-- imp 是元件实例通过v-for展示出来 -->
    <!-- stream 是一种命名为流的类 用于展示Node 和 Line -->
    <stream 
      v-for="stream in streams" :key=stream.index
      :Nodes="stream">
    </stream>
  </div>
  <right-bar
  :value="componentList[current].value"
  :ports="componentList[current].ports"
  :name="componentList[current].name"
  :type="componentList[current].type">
  </right-bar>
  </div>
</template>
<script>
import componentImp from "./componentImp.vue";
import rightBar from './rightBar.vue'
import _global from './Global.vue'
import stream  from './stream.vue'
export default {
  components: {
  componentImp,
  rightBar,
  stream },
  data(){
    return{
    current:0,
    componentList:[],
    streams:[],
      nameList:{
          Resistor:'R',
          Voltage:'V',
        },
        contextMenuData:{
          menuName:"toolbox",
          axis:{
            x:null,
            y:null
          },
          menulists:[
            {
              fnHandler:"savedata",
              btnName:"Save"
            },
            {
              fnHandler:"newdata",
              btnName:"New"
            }
          ]
        }
  }
},
  methods:{
    genComponent(type){
      console.log(type)
        let count = 0;
      this.componentList.map(function(item){
        if(item.type == type){
          count = count+1;
        }
      })
      let name = this.nameList[type] +''+count;
      const data = {
        index:this.componentList.length,
        type:type,
        name:name,
        value:100,
        ports:{
           port1:{
          to:'',
          port:''
          },
          port2:{
            to:'',
            port:''
          }
        }
        //unitType
      }
      // console.log("get ",name)
      console.log(this.componentList);
      this.componentList.push(data);//数据添加
    },
    drophandler(ev){
      console.log(ev)
      // console.log("drop")
    },
    dragover_handler(ev){
      console.log(ev)
      // console.log("dragover")
    },
    chosen(index){
      this.current = index
    },
    showMenu(data){
      // console.log(data,"data")
      console.log(data.index,"被右键")
      this.contextMenuData.axis={
        x:data.x,
        y:data.y
      }
      this.current=data.index
    },
    savedata(){
      alert("保存");
    },
    newdata(){
      alert("New");
    },
    clickHandler(){
      console.log("canvas clicked");
    },
    nodeLink(rawdata){
      const index= this.streams.length-1;
      const data = {
        Node1:{
          X:rawdata.X,
          Y:rawdata.Y
        },
        Node2:{
          X:rawdata.X,
          Y:rawdata.Y
        },
        index:index
      }
      if(_global.drawing == false){
        console.log("起点",rawdata);
        _global.drawing =true;
        this.streams.push(data);
      }else{
        
        console.log("终点",rawdata);
        _global.drawing = false;
        this.$set(this.streams[index],'Node2',{
          X:rawdata.X,
          Y:rawdata.Y
        })
      }
    },
  },
  
}
</script>
<style scoped>
  #canvas{
    flex-shrink: 0;
    width:1000px;
    height: 100%;
    background-color: white;
    position:relative
  }
</style>