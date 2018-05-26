<template>
  <div class="content">
    <div class="user" @click="goFriendHouse(index+1)" v-for="(user,index) in users" :key="index">
      <div class="ranking">{{index+1}}</div>
      <div class="head">
        <div class="mark"></div>
        <img :src="user.image" style='width:120rpx; height:120rpx;' class='head_icon'>
      </div>
      <div class="message">
        <div class="name">{{user.name}}</div>
        <div class="energy">能量值：{{user.energy}}%</div>
      </div>
      <div class="weight">{{user.weight}}kg</div>
    </div>
  </div>
</template>

<script>

export default {
  data () {
    return {
      users: [{
      image: "/copy-asset/images/hasUserInfo.jpg",
      name: 'hello',
      energy: 80,
      weight: 13.7
    }, {
      image: "/copy-asset/images/hasUserInfo.jpg",
      name: 'hello',
      energy: 80,
      weight: 13.7
    }, {
      image: "/copy-asset/images/hasUserInfo.jpg",
      name: 'hello',
      energy: 80,
      weight: 13.7
    }, {
      image: "/copy-asset/images/hasUserInfo.jpg",
      name: 'hello',
      energy: 80,
      weight: 13.7
    }, {
      image: "/copy-asset/images/hasUserInfo.jpg",
      name: 'hello',
      energy: 80,
      weight: 13.7
    }, {
      image: "/copy-asset/images/hasUserInfo.jpg",
      name: 'hello',
      energy: 80,
      weight: 13.7
    }, {
      image: "/copy-asset/images/hasUserInfo.jpg",
      name: 'hello',
      energy: 80,
      weight: 13.7
    }, {
      image: "/copy-asset/images/hasUserInfo.jpg",
      name: 'hello',
      energy: 80,
      weight: 13.7
    }]
    }
  },
  methods: {
    goFriendHouse(index){
      console.log('hello')
      wx.navigateTo({
        url:'../home/main?id='+index+'&showType=false'
      })
    }
  },
  // onShow(){
  //   //获取页面栈
  //   var pages = getCurrentPages();
  //   if(pages.length >= 1){
  //   //上一个页面实例对象
  //   var prePage = pages[pages.length - 2];
  //   console.log(prePage)
  //   //关键在这里
  //   prePage.data.$root.showType = true
  //   }
  // }
}
</script>

<style scoped>
.content {
  position: absolute;
  top: 0;
  right: 0;
  width: 100vw;
  background-color: #5dafaf;
  min-height: 100%;
  opacity: 1;
}

.user {
  display: flex;
  padding: 20rpx 0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.3);
  align-items: center;
  color: #fff;
  font-size: 30rpx;
}

.user:last-child{
  bottom: 0;
}
.ranking {
  width: 10%;
  padding-left: 30rpx;
}

.head {
  width: 20%;
  padding-top: 20rpx;
  position: relative;  
}
.mark{
  position: absolute;
  width: 30rpx;
  height: 30rpx;
  background-color: #f9a934;
  top: 20rpx;
  left: 0rpx;
  border-radius: 15px;
}
.head_icon {
  border-radius: 60rpx;
}

.message {
  width: 50%;
  padding-left: 30rpx;
}

.weight {
  width: 20%;
  text-align: right;
  padding-right: 20rpx;
}

</style>
