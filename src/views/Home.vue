<!--
 * @Author: your name
 * @Date: 2020-01-11 20:22:44
 * @LastEditTime : 2020-01-11 21:48:08
 * @LastEditors  : Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: /newyeardraw/src/views/Home.vue
 -->
<template>
  <div class="home">
    <div class="container">
      <div class="timer-container">
        <div v-for="(t,index) in time" :key="index" class="wrap">
          <div class="time" :class="`timer_${time[index]}`"></div>
        </div>
      </div>
      <div class="line"></div>
      <div class="money-container">
        <div class="money-wrap">
          <div class="money" :style="{backgroundPositionY:geY+'px'}"></div>
        </div>
        <div class="money-wrap">
          <div class="money" :style="{backgroundPositionY:shiY+'px'}"></div>
        </div>
        <div class="money-wrap">
          <div class="money" :style="{backgroundPositionY:baiY+'px'}"></div>
        </div>
        <div class="money-wrap">
          <div class="money" :style="{backgroundPositionY:qianY+'px'}"></div>
        </div>
        <div class="money-wrap">
          <div class="money" :style="{backgroundPositionY:wanY+'px'}"></div>
        </div>
        <div class="money-wrap">
          <div class="money" :style="{backgroundPositionY:shiwanY+'px'}"></div>
        </div>
      </div>
      <!-- <div class="line"></div> -->
    </div>
    <!-- <h1>{{ time }}</h1> -->
    
  </div>
</template>

<script>
export default {
  name: "home",
  data: function() {
    return {
      time: "",
      date: "",
      money:812345,
      geY:0,
      shiY:0,
      baiY:0,
      qianY:0,
      wanY:0,
      shiwanY:0,
      animTime:10,
      stop:null
    };
  },
  mounted() {
    this.updateTime()
    setInterval(this.updateTime, 1000);
    requestAnimationFrame( this.moneyAnim );
  },
  methods: {
    moneyAnim(){
      this.anim('geY',8)
      this.anim('shiY',2)
      this.anim('baiY',3)
      this.anim('qianY',4)
      this.anim('wanY',6)
      this.anim('shiwanY',0)
      this.stop = requestAnimationFrame( this.moneyAnim );
      if(this.animTime>1){
        this.animTime-=0.02
      }
    },
    anim(num,num2){
      if(this[num]>parseInt(-num2+'00')||this.animTime>1){
        this[num]-=this.animTime
      }
      
      if(this[num]<=-1000){
        this[num]= 0
      }
    },
    updateTime() {
      var cd = new Date();
      this.time =
        this.zeroPadding(cd.getHours(), 2) +
        "d" +
        this.zeroPadding(cd.getMinutes(), 2) +
        "d" +
        this.zeroPadding(cd.getSeconds(), 2);
    },
    zeroPadding(num, digit) {
      var zero = "";
      for (var i = 0; i < digit; i++) {
        zero += "0";
      }
      return (zero + num).slice(-digit);
    }
  }
};
</script>

<style scoped lang="stylus">
/* timer */
@import url('./timer.stylus');

.home {
  min-height: 100vh;
  width: 100%;
  /* background-image: url("../assets/1.png"); */
  background-size: contain;
  background-repeat: no-repeat;
  .container{
    width 1200px;
    height 750px;
    background-image url('../assets/8.png')
    background-repeat no-repeat
    background-size contain
    position: fixed;
    top: 0;
    left: 50%;
    margin-left: -600px;
  }
  .wrap{
    display: flex;
    justify-content: center;
    align-items center;
    background: url('../assets/1.png') no-repeat -259px -70px;
    width: 83px;
    height: 107px;
    margin-right 4px;
  }
}
.money-container {
  transform: scale(0.85);
  margin 0 auto;
	background: url('../assets/1.png') no-repeat -544px -62px;
	width: 528px;
	height: 125px;
  display flex
  align-items center
  justify-content space-evenly
  padding:0px 30px;
  box-sizing: border-box;
  .money-wrap{
    background: url('../assets/1.png') no-repeat -405px -77px;
    width: 71px;
    height: 93px;
    display flex;
    align-items center;
    justify-content center
    .money{
      background: url('../assets/money.png') no-repeat -9px -0px;
      width: 67px;
      height: 85px;
      // transition: all 10000ms cubic-bezier(0.150, 0.450, 0.000, 0.940); 
      margin-top: -6px;
      // animation:money 5s linear infinite
    }
  }
}
@keyframes money {
  0%{
    background-position-y 0
  }
  100%{
    background-position-y -1000px
  }
}
.line {
  margin-top 14px;
	background: url('../assets/1.png') no-repeat 0 -308px;
	width: 100%;
	height: 9px;
}


.time{
  /* flex: 1; */
}
.timer-container{
  transform: scale(0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top 140px;
}


</style>
