<template>
  <div>
    <img class="background" alt="背景" src="./assets/img1.png">
    <div class="bottom">
      <div class="Left">
        <img class="wechat" alt="微信" src="./assets/wechat.png">
        加老师微信：<span>vip_shoushen697</span><br>
        <span>【点击复制微信号】</span>现在就是最低价~
      </div>
      <div class="Right" @click="getTicket">
        <img class="finger" alt="立即领取" src="./assets/btn.jpg">
      </div>
    </div>
    <Window v-if="isShow" @hide="hide"/>
  </div>
</template>

<script>
import Window from './components/window.vue'

export default {
  name: 'Index',
  data () {
    return {
      isShow: false
    }
  },
  mounted () {
  },
  methods: {
    getTicket () {
      this.isShow = true
    },
    hide () {
      this.isShow = false
    }
  },
  components: {
    Window
  }
}
</script>

<style lang="scss" scoped>
.background{
  width: 100%;
  margin: 0 0 80px 0;
  border: 0;
}
.bottom{
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  z-index: 1;
  height: 80px;
  background-color: red;
  .Left{
    box-sizing: border-box;
    padding: 10px 10px;
    float: left;
    color: white;
    font-size: 12px;
    line-height: 30px;
    span {
      color:yellow;
    }
    .wechat{
      width: 20px;
      height: 15px;
    }
  }
  .Right {
    box-sizing: border-box;
    padding: 10px 10px;
    float: right;
    .finger {
      border-radius: 10px; 
      height: 60px;
      width: 60px;
    }
  }
}
.clear{
  clear: both;
}

</style>
