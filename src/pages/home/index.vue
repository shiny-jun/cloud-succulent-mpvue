<template>
  <div class="home">
    <div class="background_icon">
      <div class="sun"><img src="../../images/sun.png" style='width:120rpx;height:120rpx;'></div>
      <div class="cloud">
        <img src="../../images/cloud.png" class="cloud1" style='width:120rpx;height:120rpx;'>
        <img src="../../images/cloud.png" class="cloud2" style='width:150rpx;height:150rpx;'>
      </div>
      <div class="bee">
        <img src="../../images/bee.png" style='width:40rpx;height:40rpx;'>
      </div>
    </div>
    <div class="point" v-if="!showType">积分:{{point}}</div>
    <div class="point" v-else>{{userName}}的肉肉</div>
    <div class="regulation">
      <a href="/pages/help/main">
        <img src="../../images/regulation.png" style='width:50rpx;height:50rpx;' class='regulation_icon'>
      </a>
    </div>
    <div class="energy_message">
      <a href="/pages/message/main">
        <img src="../../images/message.png" style='width:60rpx;height:60rpx;' class='energy_icon box-shadow1'>
      </a>
    </div>
    <div class="water">
      <img :src="waterImg" style='width:100rpx;height:100rpx;'>
      <div class="condition">
        <div>{{percent}}%</div>
        <div>容量:{{weight}}g</div>
      </div>
    </div>
    <div class="plant">
      <img :src="rourouImg" @click="touchPlant" style="width:440rpx;height:440rpx;">
    </div>
    <div class="users" @click="goUsersList" v-if="!showType">
        <img src="../../images/users.png" style='width:60rpx;height:60rpx;' class='user_icon box-shadow'>
    </div>
    <div class="users" @click="goHome" v-else>
        <img src="../../images/home.png" style='width:60rpx;height:60rpx;' class='user_icon box-shadow'>
    </div>
  </div>
</template>

<script>
const rourouImgs = [
  "https://cloud-minapp-14328.cloud.ifanrusercontent.com/1fM84HuLorguPFIf.png",
  "https://cloud-minapp-14328.cloud.ifanrusercontent.com/1fM84HlysWtirdKl.png",
  "https://cloud-minapp-14328.cloud.ifanrusercontent.com/1fM84HNGbyoLMPrD.png",
  "https://cloud-minapp-14328.cloud.ifanrusercontent.com/1fM84HmnGmNvgKib.png",
  "https://cloud-minapp-14328.cloud.ifanrusercontent.com/1fM84HYFMATGJbsf.png",
  "https://cloud-minapp-14328.cloud.ifanrusercontent.com/1fM84HKPWDKtwbsd.png"
];
const waterImgs = [
  "https://cloud-minapp-14328.cloud.ifanrusercontent.com/1fMBdlJfpmyUIkjv.png",
  "https://cloud-minapp-14328.cloud.ifanrusercontent.com/1fMBdlnafkTxNGAw.png",
  "https://cloud-minapp-14328.cloud.ifanrusercontent.com/1fMBdlojRIWscYmA.png",
  "https://cloud-minapp-14328.cloud.ifanrusercontent.com/1fMBdlYvPBpzoZYe.png",
  "https://cloud-minapp-14328.cloud.ifanrusercontent.com/1fMBdlUtbLydUnOE.png",
  "https://cloud-minapp-14328.cloud.ifanrusercontent.com/1fMBdlPhZvhYqOPO.png",
  "https://cloud-minapp-14328.cloud.ifanrusercontent.com/1fMBdlHoaJGgCSuU.png",
  "https://cloud-minapp-14328.cloud.ifanrusercontent.com/1fMBdlUpUcsNKnhf.png",
  "https://cloud-minapp-14328.cloud.ifanrusercontent.com/1fMBdlJKmamrYtJt.png"
];
export default {
  data() {
    return {
      point: 300,
      percent: 70,
      weight: 30,
      open: false,
      docked: true,
      rourouImg:
        "https://cloud-minapp-14328.cloud.ifanrusercontent.com/1fM84HuLorguPFIf.png",
      waterImg:
        "https://cloud-minapp-14328.cloud.ifanrusercontent.com/1fMBdlJfpmyUIkjv.png",
      grow: 70,
      showType:true, // showType:true为自己房间，false为朋友房间
      userName:'hello'
    };
  },
  methods: {
    bindViewTap() {
      const url = "../logs/main";
      wx.navigateTo({ url });
    },
    getUserInfo() {
      // 调用登录接口
      wx.login({
        success: () => {
          wx.getUserInfo({
            success: res => {
              this.userInfo = res.userInfo;
            }
          });
        }
      });
    },
    getrourouImg(grow) {
      let rourou = "";
      for (let i in rourouImgs) {
        if (grow <= (Number(i) + 1) * 20) {
          rourou = rourouImgs[i];
          break;
        }
      }
      return rourou;
    },
    getwaterImg(percent) {
      let water = "";
      for (let i in waterImgs) {
        console.log(percent)
        if (percent*10 <= (Number(i) + 1) * 125) {
          water = waterImgs[i];
          break;
        }
      }
      return water;
    },
    goHome(){
      var pages = getCurrentPages();
      if(pages.length >= 2){
      //上一个页面实例对象
        var prePage = pages[pages.length - 3];
        console.log(prePage)
      //关键在这里
        prePage.data.$root[0].showType = true
        wx.navigateBack({
          delta:2
        })
      }
      
      
    },
    goUsersList(){
      wx.navigateTo({
        url:'../usersList/main'
      })
    }
  },
  mounted () {
    // 调用应用实例的方法获取全局数据
    let grow = this.grow;
    this.rourouImg = this.getrourouImg(grow);
    let percent = this.percent;
    this.waterImg = this.getwaterImg(percent);
    // this.showType = true
    this.userName = this.$root.$mp.query.id
    this.showType = this.$root.$mp.query.showType
    this.$root.$mp.query = null
  }
};
</script>

<style scoped>
.home {
  height: 100vh;
  background: #aff1fd
    url("https://cloud-minapp-14328.cloud.ifanrusercontent.com/1fM7jTVYhOPucHzt.jpg")
    0 0 no-repeat;
  background-size: 750rpx 100%;
}
.content {
  /* display: none; */
  min-height: 100%;
}
.sun {
  position: absolute;
  top: 40rpx;
  left: 80rpx;
}

.cloud2 {
  position: absolute;
  top: 100rpx;
  right: 200rpx;
}
.point {
  width: 100vw;
  font-weight: bold;
  text-align: center;
  font-size: 30rpx;
  color: #2e716a;
  padding-top: 20rpx;
}
.regulation {
  position: absolute;
  top: 20rpx;
  right: 40rpx;
}
.energy_message {
  position: absolute;
  bottom: 40rpx;
  right: 40rpx;
}
.energy_icon {
  background-color: #b7dd7a;
  padding: 20rpx;
  border-radius: 50rpx;
}
.water {
  display: flex;
  position: absolute;
  bottom: 40rpx;
  left: 160rpx;
  align-items: center;
  height: 120rpx;
}

.condition {
  font-size: 30rpx;
  color: white;
}

.plant {
  position: absolute;
  bottom: 350rpx;
  left: 170rpx;
}

.users {
  position: absolute;
  left: 40rpx;
  bottom: 40rpx;
}

.user_icon {
  background-color: #f9a934;
  padding: 20rpx;
  border-radius: 50rpx;
}

.box-shadow {
  -webkit-box-shadow: 2px 2px 2px #ab7931;  
  -moz-box-shadow: 2px 2px 2px #ab7931;  
  box-shadow: 2px 2px 2px #ab7931;
}
.box-shadow1 {
  box-shadow: 2px 2px 2px #98b767;
}
.scroll-view-item_H {
  text-align: center;
  height: 47px;
  line-height: 45px;
}

.bee
{
  position: absolute;
  left:250px; 
  top:170px;
  transform: rotate(-80deg);
	animation-name:mybee;
	animation-duration:4s;
	animation-timing-function:linear;
	animation-iteration-count:infinite;
	animation-direction:initial;
	animation-play-state:running;
	/* Safari and Chrome: */
	-webkit-animation-name:mybee;
	-webkit-animation-duration:4s;
	-webkit-animation-timing-function:linear;
	-webkit-animation-iteration-count:infinite;
	-webkit-animation-direction:initial;
	-webkit-animation-play-state:running;
}

@keyframes mybee
{
	0%   {left:250px; top:170px; transform: rotate(-80deg)}
	20%   {left:180px; top:190px; transform: rotate(-80deg)}
	25%  {left:170px; top:190px; transform: rotate(0deg)}
	40%  {left:120px; top:175px; transform: rotate(0deg)}
	50%  {left:120px; top:170px; transform: rotate(120deg)}
	66%  {left:160px; top:165px; transform: rotate(120deg)}
	70%  {left:170px; top:165px; transform: rotate(90deg)}
	85%  {left:210px; top:150px; transform: rotate(90deg)}
	87%  {left:220px; top:150px; transform: rotate(30deg)}
	100% {left:250px; top:170px; transform: rotate(-80deg)}
}
/* Safari and Chrome */
@-webkit-keyframes mybee {
	0%   {left:250px; top:170px; transform: rotate(-80deg)}
	20%   {left:180px; top:190px; transform: rotate(-80deg)}
	25%  {left:170px; top:190px; transform: rotate(0deg)}
	40%  {left:120px; top:175px; transform: rotate(0deg)}
	50%  {left:120px; top:170px; transform: rotate(120deg)}
	66%  {left:160px; top:165px; transform: rotate(120deg)}
	70%  {left:170px; top:165px; transform: rotate(90deg)}
	85%  {left:210px; top:150px; transform: rotate(90deg)}
	87%  {left:220px; top:150px; transform: rotate(30deg)}
	100% {left:250px; top:170px; transform: rotate(-80deg)}
}
.cloud1{
  position: absolute;
  top: 60rpx;
  left: 150rpx;
	animation-name:mycloud1;
	animation-duration:3s;
	animation-timing-function:linear;
	animation-iteration-count:infinite;
	animation-direction:initial;
	animation-play-state:running;
	/* Safari and Chrome: */
	-webkit-animation-name:mycloud1;
	-webkit-animation-duration:3s;
	-webkit-animation-iteration-count:infinite;
	-webkit-animation-direction:initial;
	-webkit-animation-play-state:running;
}
@keyframes mycloud1{
	0%   {top: 60rpx;left: 150rpx;}
	50%  {top: 60rpx;left: 170rpx;}
	100%   {top: 60rpx;left: 150rpx;}
}
/* Safari and Chrome */
@-webkit-keyframes mycloud1 {
	0%   {top: 60rpx;left: 150rpx;}
	50%  {top: 60rpx;left: 170rpx;}
	100%   {top: 60rpx;left: 150rpx;}
}

.cloud2 {
  position: absolute;
  top: 100rpx;
  right: 200rpx;
  animation-name:mycloud2;
	animation-duration:3s;
	animation-timing-function:linear;
	animation-iteration-count:infinite;
	animation-direction:initial;
	animation-play-state:running;
	/* Safari and Chrome: */
	-webkit-animation-name:mycloud2;
	-webkit-animation-duration:3s;
	-webkit-animation-timing-function:linear;
	-webkit-animation-iteration-count:infinite;
	-webkit-animation-direction:initial;
	-webkit-animation-play-state:running;
}
@keyframes mycloud2{
	0%   {top: 100rpx;right: 200rpx;}
	50%  {top: 100rpx;right: 170rpx;}
	100%   {top: 100rpx;right: 200rpx;}
}
/* Safari and Chrome */
@-webkit-keyframes mycloud2 {
	0%   {top: 100rpx;right: 200rpx;}
	50%  {top: 100rpx;right: 170rpx;}
	100% {top: 100rpx;right: 200rpx;}
}
</style>
