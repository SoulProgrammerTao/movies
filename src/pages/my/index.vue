<template>
  <div class="my">
    <div class="top">
      <div class="itme" @click="goOrder">
        <span>我的订单</span>
        <img src="../../../static/images/left.png" alt="">
      </div>
      <div class="itme" @click="goPay">
        <span>优惠券/支付</span>
        <img src="../../../static/images/left.png" alt="">
      </div>
      <div class="itme">
        <span>影院会员卡</span>
        <img src="../../../static/images/left.png" alt="">
      </div>
    </div>
    <div class="bottom">
      <div class="itme" @click="goCollection">
        <span>收藏的电影</span>
        <img src="../../../static/images/left.png" alt="">
      </div>
      <div class="itme">
        <span>看过的电影</span>
        <img src="../../../static/images/left.png" alt="">
      </div>
    </div>
  </div>
</template>

<script>

export default {
  methods: {
    goOrder () {
      wx.navigateTo({
        url: '/pages/order/main'
      })
    },
    goCollection () {
      wx.navigateTo({
        url: '/pages/collection/main'
      })
    },
    goPay () {
      wx.navigateTo({
        url: '/pages/pay/main'
      })
    }
  }
}
</script>

<style>
.my {
  background: #f5f5f5;
  height: 100%;
  padding-top: 10px;
}
.top {
  background-color: #fff;
}
.itme {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 50px;
  padding: 0 15px;
  border-bottom: #f5f5f5 1px solid;
}
.itme > img {
  width: 14px;
  height: 18px;
}
.bottom {
  margin-top: 10px;
  background-color: #fff;
}
</style>
