<template>
  <div class="window">
    <div class="mask" @click="hide"></div>
    <div class="content flex_col">
      <div class="title flex_row_c">
        <img src="../assets/success.png" alt="领券成功">恭喜领券成功
      </div>
      <div class="title2 flex_row_c">
        <span>￥{{ticket}}</span>代金券
      </div>
      <div class="desc">
        <div class="title">
          使用代金券支付以下商品，既可<b>立享优惠</b>
        </div>
        <div class="text">
          <b>温馨提示：</b>本券为“天马生活”会员专属代金券，店内使用该券无效。请在30分钟内完成付款。
        </div>
      </div>
      <div class="details flex_row_b">
        <img :src="procuct.img">
        <div class="text_con flex_col_s">
          <div class="name">
            {{procuct.name}}
          </div>
          <div class="price">
            ￥<span>{{procuct.price}}</span> 门店价
          </div>
          <div class="tips">
            可使用<span>{{ticket}} 代金券</span>{{ticketNum}}张
          </div>
        </div>
      </div>
      <div class="num_con flex_row_b">
        <div class="label flex_row_b">
          <span>数</span><span>量</span>
        </div>
        <div class="num flex_row_c">
          <div class="block" @click="less">-</div>
          <input type="number" v-model="num">
          <div class="block" @click="plus">+</div>
        </div>
      </div>
      <div class="user_con flex_row_b">
        <div class="label flex_row_b">
          <span>购</span><span>买</span><span>人</span>
        </div>
        <input type="text" placeholder="请输入购买人姓名" v-model="name">
      </div>
      <div class="phone flex_row_b">
        <div class="label">
          联系方式
        </div>
        <input type="text" placeholder="请输入购买人手机" v-model="phone" @blur="checkPhone" :class="isPhone?'ss':'error'">
      </div>
      <div class="money flex_row_b">
        <div class="label">
          支付金额
        </div>
        <div class="money">
          {{money}}元
        </div>
      </div>
      <div class="pay_con">
        <div class="title">
          支付方式
        </div>
        <div class="way">
          <div class="item flex_row_b" v-for="(item, index) in payWay" :key="index" @click="choosePayWay(item)">
            <div class="type">
              <img :src="item.img" class="tag">
              {{item.label}}
            </div>
            <img src="../assets/gou.png" class="" :class="item.isChoosed?'':'grey'">
          </div>
        </div>
      </div>
      <div class="pay_btn" :class="isPayReady?'':'grey'" @click="chooseUse()">
        使用代金券支付
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: '',
  data () {
    return {
      ticket: 900,
      ticketNum: 1,
      price: 1199,
      num: 0,
      phone: '',
      name: '',
      isPhone: true,
      procuct: {
        img: require('../assets/img.jpg'),
        name: '【爱儿美】超值单人儿童写真拍摄套餐',
        price: '1199'
      },
      payWay: [{
        img: require('../assets/pay.png'),
        label: '微信支付',
        isChoosed: false,
      }],
    }
  },
  computed: {
    money () {
      let money = (this.price * this.num) - (this.ticket * this.ticketNum)
      return money 
    },
    isPayReady () {
      let isPayChoosed = false
      this.payWay.map((i) => {
        if (i.isChoosed) {
          isPayChoosed = true
        }
      })
      return isPayChoosed
    }
  },
  methods: {
    less () {
      if(this.num > 0){
        this.num--
      }
    },
    plus () {
      return this.num++
    },
    choosePayWay (item) {
      item.isChoosed = !item.isChoosed
    },
    checkPhone () {
      let reg = /^1[3456789]\d{9}$/
      this.isPhone = reg.test(this.phone)
      console.log(this.isPhone)
      return this.isPhone
    },
    hide () {
      this.$emit('hide')
    },
    chooseUse(){
        if(!this.isPayReady){
          alert("请选择支付方式");
          return
        }
        if(this.num == 0){
          alert("请添加数量");
          return
        }
        if(this.name == ''){
          alert("请填写购买人");
          return
        }
        if(this.phone == ''){
          alert("请填写联系方式");
          return
        }
        {alert("提交成功")}
    }
  }
}
</script>

<style lang="scss" scoped>
.window {
  position: fixed;
  z-index: 10;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  .mask {
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 11;
    position: fixed;
    background: rgba(15, 8, 8, 0.699);
  }
  .content {
    z-index: 21;
    position: fixed;
    transform: translate(-50%, -50%);
    left: 50%;
    top: 50%;
    box-sizing: border-box;
    display: block;
    width: 90%;
    height: 90%;
    background: #fff;
    border-radius: 5px;
    overflow-y: scroll;
    .title {
      margin: 30px 0 0;
      font-size: 24px;
      img {
        margin: 0 10px 0 0;
        width: 30px;
        height: 30px;
      }
    }
    .title2 {
      margin: 15px auto 0;
      line-height: 30px;
      font-size: 20px;
      span {
        margin: 0 10px 0 0;
        color:rgb(238, 87, 87);
        font-size: 26px;
        font-weight: bold;
        line-height: 26px;
      }
    }
    .desc {
      width: 90%;
      margin: 15px auto 0;
      background-color:rgb(250, 239, 239);
      .title {
        color:rgb(235, 107, 107);
        font-size: 15px;
        padding: 15px;
      }
      .text {
        color:rgba(0, 0, 0, 0.432);
        font-size: 15px;
        padding: 0 15px 15px 15px;
      }
    }
    .details {
      width: 90%;
      margin: 15px auto 0;
      background:rgb(248, 246, 246);
      border-radius: 4px;
      img {
        margin: 0 10px 0 0;
        width: 120px;
        height: 120px;
      }
      .text_con {
        .name {
          font-size: 15px;
          color:rgb(136, 130, 130);
        }
        .price {
          color:rgb(136, 130, 130);
          font-size: 9px;
          line-height: 30px;
          border-bottom: 1px #aaa dashed;
          span {
          font-size: 15px;
          color:rgb(71, 70, 70);
          font-weight: 520;
          }
        }
        .tips {
          font-size: 14px;
          color:rgb(238, 87, 87);
          line-height: 35px;
          span {
            font-size: 14px;
            font-weight: 1000;
          }
        }
      }
    }
    .num_con {
      width: 90%;
      margin: 15px auto 0;
      .label {
        width: 60px;
      }
      .num {
        width: 120px;
        .block {
          width: 20px;
          text-align: center;
          border: 1px #ccc solid;
          font-size: 16px;
          color:rgb(161, 159, 159);
        }
        input {
          text-align: center;
          margin: 0 2px;
          width: 70px;
          height:20px;
          border: 1px #ccc solid;
        }
        
      }
    }
    .user_con {
      width: 90%;
      margin: 15px auto 0;
      .label {
        width: 60px;
      }
      input {
        width: 160px;
        height: 20px;
        padding: 7px;
        border: 1px #ccc solid;
        border-radius: 5px; 
      }
    }
    .phone {
      width: 90%;
      margin: 15px auto 0;
      .label {
        width: 80px;
      }
      input {
        width: 160px;
        height: 20px;
        padding: 7px;
        border: 1px #ccc solid;
        border-radius: 5px; 
      }
    }
    .money {
      width: 90%;
      margin: 15px auto 0;
      .label {
        line-height: 20px;
        width: 100px;
        height: 10px;
      }
      .money {
        line-height: 20px;
        text-align:right;
        color:red;
      }
    }
    .pay_con {
      width: 90%;
      margin: 25px auto 20px;
      .title {
        width: 100%;
        margin: 0 auto;
        border-left: red 6px solid;
        line-height: 13px;
        padding: 5px;
        font-size: 17px;
        font-weight: 600;
      }
      .way {
        margin: 20px auto 0;
        .item {
          .type {
            img {
            width: 17px;
            }
          }
          img {
          width: 20px;
          }
        }
      }
    }
    .pay_btn {
      width: 100%;
      height: 50px;
      line-height: 50px;
      background: red;
      color: #fff;
      text-align: center;
      font-size: 24px;
    }
    .grey {
      filter: grayscale(100%); 
      opacity: 0.6;
    }
    .error {
      border: 1px solid red;
    }
  }
}
.flex_col {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;

}
.flex_col_s {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: stat;

}
.flex_row_c {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  
}
.flex_row_b {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  
}
</style>