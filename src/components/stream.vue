<template>
  <div class="stream" :style={width:WIDTH,height:HEIGHT}>
    <img :width="WIDTH" class="horizontal" height="10" :src="require(`../assets/line.png`)">
    <img  :width="HEIGHT" class="vertical" height="10" :src="require(`../assets/line.png`)" >
  </div>
</template>
<script>
export default {
  mounted(){
     console.log("streamCreating");
     const stream = this.$el;
     const n1 =this.Nodes.Node1;
     const n2 =this.Nodes.Node2;
     stream.style.left = (Math.min(n1.X,n2.X)-1)*10+'px';
     stream.style.top = (Math.min(n1.Y,n2.Y)-1)*10+'px';
  },
  props:{
    Nodes:Object
  },
  computed:{
    WIDTH(){
      return (this.Nodes.Node1.X-this.Nodes.Node2.X+1)*10+'px';
    },
    HEIGHT(){
      return (this.Nodes.Node1.Y-this.Nodes.Node2.Y+1)*10+'px';
    }
  }
}
</script>
<style scoped>
.stream{
  position: absolute;
}
img{
  position: absolute;
}
.horizontal{
  bottom: 0;
}
.vertical{
  right: 0;
  transform: rotate(90deg)
}
</style>