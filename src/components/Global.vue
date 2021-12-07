<script>
let drawing = false;
export default {
  drawing,
  px2pixiv(length){//一个将px转换为格子数的工具(10*(n-1)+1,10*n)
      if(length%0==0){
        return length/10;
      }else{
        return Math.floor(length/10)+1;
      }
    }
}
//全局变量模块
</script>