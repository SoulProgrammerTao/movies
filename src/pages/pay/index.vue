<template>
  <div class="pay">
    <p class="date">1天后开场</p>
    <p class="tip">凭二维码取票更方便，取票码将以短信形式发送</p>
    <div class="container">
      <div class="header">
        <div class="left">
          <p class="title">{{orderInfo.title}}</p>
          <p class="dt">明天 12-19 15:45 ~ 17:20(国语3D)</p>
          <p class="ad">天堂影院皇后大道店 8号厅</p>
          <p class="wz">5排3座</p>
        </div>
        <img class="pic" :src="orderInfo.images.small" alt="">
      </div>
      <div class="footer">
        <p class="qp">取票二维码</p>
        <img class="code" src="../../../static/images/code.png" alt="">
      </div>
    </div>
  </div>
</template>

<script>

export default {
  data () {
    return {
      orderInfo: {}
    }
  },
  beforeMount() {
    wx.getStorage({
      key: 'detail',
      success: (res) => {
        this.orderInfo = res.data
      },
    })
  },
  methods: {
  }
}
</script>

<style>
.pay {
  width: 100%;
  height: 100%;
  overflow: hidden;
  background-color: #414640;
  padding: 0 10px;
}
.pay .date {
  font-size: 20px;
  color: #fff;
  text-align: center;
  margin-top: 15px;
}
.pay .tip {
  color: #fff;
  text-align: center;
  margin-top: 20px;
}
.pay .container {
  margin-top: 30px;
  background-color: #fff;
  padding: 30px;
}
.pay .header {
  display: flex;
  border-bottom: 1px solid #666;
  padding-bottom: 10px;
}
.pay .left {
  flex: 1;
  margin-right: 15px;
}
.pay .pic {
  width: 76px;
  height: 107px;
}
.pay .title {
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 10px;
}
.pay .dt,.ad,.wz {
  font-size: 14px;
  color: #666;
}
.pay .footer {
  padding-top: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.pay .qp {
  font-size: 18px;
  font-weight: bold;
}
.pay .code {
  width: 250px;
  height: 250px;
  margin: 20px auto;
}
</style>
