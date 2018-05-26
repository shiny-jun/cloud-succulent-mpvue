<template>
  <div>
    <div class="content">
      <div class="log" v-for="(log,index) in logs" :key="index">
        <div class="date">{{log.date}}</div>
        <div class="message">
          <div class="message-item" v-for="(message,index2) in log.messages" :key="index2">
            <div class="type">
              <img src="../../images/pinch2.png" style="width:50rpx;height:50rpx;"/>
            </div>
            <div class="name">
              <span>{{message.name}}</span>收取了{{message.getWeight}}g
            </div>
            <div class="time">{{message.hour}}:{{message.minute}}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  data () {
    return {
      logs:[{
      date:'今天',
      messages:[{
        name:'范冰冰',
        getWeight:2,
        hour:12,
        minute:30
      },{
        name:'范冰冰',
        getWeight:2,
        hour:12,
        minute:30
      },{
        name:'范冰冰',
        getWeight:2,
        hour:12,
        minute:30
      }]
    },{
      date:'昨天',
      messages:[{
        name: '范冰冰',
        getWeight: 2,
        hour: 12,
        minute: 30
      }, {
        name: '范冰冰',
        getWeight: 2,
        hour: 12,
        minute: 30
      },{
        name: '范冰冰',
        getWeight: 2,
        hour: 12,
        minute: 30
      }]
    },{
      date:'5-20',
      messages:[{
        name: '范冰冰',
        getWeight: 2,
        hour: 12,
        minute: 30
      }, {
        name: '范冰冰',
        getWeight: 2,
        hour: 12,
        minute: 30
      },{
        name: '范冰冰',
        getWeight: 2,
        hour: 12,
        minute: 30
      }]
    }]
    }
  },

  created () {
    // 调用应用实例的方法获取全局数据
  }
}
</script>

<style scoped>
.content {
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  background-color: #5dafaf;
  min-height: 100%;
  opacity: 1;
}

.scroll-view_H {
  height: 100vh;
  white-space: nowrap;
}

.log{
  padding: 20rpx;
  padding-bottom: 0px;
}
.date{
  font-size: 36rpx;
  font-weight: bold;
  color: white;
  margin-bottom: 10rpx;
}

.message{
  margin-left: 30rpx;
  border-left: 1rpx solid rgba(255, 255, 255, 0.5);
  padding-top: 10rpx;
}
.message-item{
  display: flex;
  position: relative;
  left: -25rpx;
  padding: 15rpx 0;
  font-size: 30rpx;
  color: #ffc878;
}
.type{
  width: 15%;
}
.type img{
  background-color: #fff;
  border-radius: 25rpx;
}
.name{
  width: 65%;
}
.name span{
  font-weight: bold;
  padding-right: 6rpx;
}
.time{
  width: 20%;
  text-align: right;
  color: white
}
</style>
