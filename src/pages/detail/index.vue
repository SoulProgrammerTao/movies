<template>
  <div class="detail">
    <div class="top">
      <img class="sl-img" :src="detail.images.small" alt="">
      <div class="right">
        <p>{{detail.title}}</p>
        <p>主演：
          <span v-for="(item1, index1) in detail.casts" :key="index1">{{item1.name}}</span>
        </p>
        <p>类型：
          <span v-for="(item1, index1) in detail.genres" :key="index1">{{item1}}</span>
        </p>
        <p>时长：
          <span v-for="(item1, index1) in detail.durations" :key="index1">{{item1}}</span>
        </p>
      </div>
    </div>
    <div class="bottom">
      <p class="desi">电影简介</p>
      <p class="lako">亦称电影故事。电影文学剧本创作前的概要描述。电影剧作者在创作电影文学剧本之前，先选用自己掌握的生活素材中最能确切表现人物性格和展示主题的一系列事件，构造成一个有简略剧情内容的故事梗概，作为进一步编写电影文学剧本的依据。它的基本内容包括主要人物、时间地点、情节发展和结局等。电影制片厂在物色剧本的阶段,往往先要剧作者交出一个故事梗概,作为评断和取舍的依据。</p>
    </div>
    <div class="bott-btn">
      <img v-if="isWant" src="../../../static/images/xiangkan2.png" alt="" @click="collection">
      <img v-else src="../../../static/images/xiangkan.png" alt="" @click="collection">
      <button @click="buy">立即购票</button>
    </div>
  </div>
</template>

<script>

export default {
  data () {
    return {
      detail: {},
      isWant: false,
      colList: [],
      ordList: []
    }
  },
  beforeMount() {
    this.isWant = false
    wx.getStorage({
      key: 'detail',
      success: (res) => {
        this.detail = res.data
      },
    })
    wx.getStorage({
      key: 'colList',
      success: (res) => {
        this.colList = res.data
      },
      fail: () => {
        this.colList = []
      }
    })
    wx.getStorage({
      key: 'ordList',
      success: (res) => {
        this.ordList = res.data
      },
      fail: () => {
        this.ordList = []
      }
    })
  },
  methods: {
    collection () {
      this.isWant = !this.isWant
      if (this.isWant && !this.colList.find(item => item.id === this.detail.id)) {
        this.colList.push(this.detail)
      }
      if (!this.isWant) {
        const index = this.colList.findIndex(item => item.id === this.detail.id)
        this.colList.splice(index, 1)
      }
    },
    buy () {
      this.ordList.push(this.detail)
      wx.setStorage({
        key: 'ordList',
        data: this.ordList
      })
      wx.navigateTo({
        url: `/pages/pay/main`
      })
    }
  },
  onUnload () {
    wx.setStorage({
      key: 'colList',
      data: this.colList
    })
  },
}
</script>

<style>
.bott-btn {
  position: absolute;
  left: 0;
  bottom: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 60px;
  width: 100%;
  padding: 30px;
}
.bott-btn > img {
  width: 30px;
  height: 30px;
}
.bott-btn > button {
  width: 150px;
  height: 50px;
  line-height: 50px;
  text-align: center;
  font-style: 20px;
  color: #fff;
  background-color: #d92812;
}
.detail {
  height: 100%;
  background-color: #f5f5f5;
  padding: 10px;
  width: 100%;
  overflow-x: hidden;
  box-sizing: border-box;
}
.bottom {
  background-color: #fff;
  margin-top: 10px;
  border-top: 1px solid #e2e2e2;
  padding: 10px;
}
.desi {
  font-size: 18px;
  padding-top: 10px;
}
.lako {
  margin-top: 10px;
}
.top {
  border-bottom: 1px solid #e2e2e2;
  height: 200px;
  display: flex;
  padding: 15px;
  background-color: #fff;
  box-sizing: border-box;
}
.sl-img {
  width: 130px;
  height: 170px;
}
.right {
  flex: 1;
  padding-left: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  overflow: hidden;
}

</style>
