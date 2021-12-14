<template>
  <div class="home">
    <div class="operate">
      <div class="resert" @click="resertCars"><span>预约用车</span></div>
      <i @click="toUser" class="user el-icon-user-solid"></i>
    </div>
    <div class="main-content">
      <div id="container">
      </div>
    </div>
    <div id="userRouter" class="user-router" :class="{open:openRight}">
        <router-view>
        </router-view>
      </div>
    
  </div>
</template>

<script>
export default {
  data () {
    return {
      openRight: false
    }
  },
  watch:{
    $route(val){
      console.log(val);
      console.log(val.name!=='Home');
      if(val.name!=='Home'){
        this.openRight = true
      }else{
        this.openRight = false
      }
      console.log('this.openRight',this.openRight);
    },
  },
  mounted() {
    this.initMap()
    this.clickOtherbackHome()
  },
  methods: {
    clickOtherbackHome(){
      document.addEventListener('mouseup', e =>{
        const userCon = document.querySelector('#userRouter')
        // if(e.target !== userCon){
        //   this.$router.push('/')
        // }
         if(!userCon.contains(e.target)){
          this.$router.push('/')
        }
      })
    },
    initMap(){
       var map = new AMap.Map('container', {
        center: [116.397428, 39.90923],
        zooms: [4,18],//设置地图级别范围
        zoom: 13
    });
    },
    resertCars(){
      this.$message.success('未处理该事件')
    },
    toUser(){
      if(!this.openRight){
        this.$router.push('/user')
      }else{
        this.$router.push('/')
      }
        
      
    },
  },
  created () {}
}
</script>

<style lang="less" scoped>
.home{
  position: relative;
  #container {width:100%; height: 100vh; }  
  .operate{
    display: flex;
    justify-content: flex-start;
    align-items: center;
    position: absolute;
    bottom: 40px;
    left: 50%;
    margin-left: -85px;
    z-index: 12;
    .resert{
      width: 150px;
      height: 30px;
      line-height: 30px;
      background-color: rgba(44, 62, 80);
      border-radius: 25px;
      cursor: pointer;
      span{
        color: antiquewhite;
      }
    }
    .user{
        margin-left: 10px;
        cursor: pointer;
      }
  }
  .user-router{
    position: fixed;
    width: 300px;
    top: 0;
    right: -300px;
    bottom: 0;
    z-index: 99;
    background-color: red;
    transition: all 1s;
  }
  .open{
    right: 0
  }
  .main-content{
    display: flex;
    justify-content: flex-start;
  }
}
</style>
