<template>
  <div class="order">
    <div class="hot-list">
      <div class="hot-item" v-for="(item,index) in orderList" :key="index">
        <img :src="item.images.small" alt="">
        <div class="hot-detl">
          <p class="hot-name">{{item.title}}</p>
          <p class="hot-yy">主演：
            <span v-for="(item1, index1) in item.casts" :key="index1">{{item1.name}}</span>
          </p>
          <p class="hot-yy">
            <span v-for="(item2, index2) in item.genres" :key="index2">{{item2}}</span>
          </p>
          <p class="hot-yy">{{item.pubdates[0]}}</p>
        </div>
        <div class="but">
          <button class="buy" @click="handleDel(index)">删除</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  data () {
    return {
      orderList: []

    }
  },
  beforeMount() {
    wx.getStorage({
      key: 'ordList',
      success: (res) => {
        this.orderList = res.data
      }
    })
  },
  methods: {
    handleDel (index) {
      this.orderList.splice(index, 1)
    }
  },
  onUnload () {
    wx.setStorage({
      key: 'ordList',
      data: this.orderList
    })
  }
}
</script>

<style>
.mgb {
  margin-bottom: 10px;
}
.hot-list {
  padding: 0 10px;
}
.hot-item {
  display: flex;
  align-items: center;
  padding: 10px 0;
  border-bottom: 1px solid #e2e2e2;
}
.hot-detl {
  flex: 1;
  padding-left: 10px;
  overflow: hidden;
}
.hot-item > img {
  width: 70px;
  height: 100px;
}
.hot-name {
  font-size: 20px;
  white-space: nowrap;
  overflow: hidden;
}
.hot-yy {
  height: 25px;
  line-height: 25px;
  color: #999;
  white-space: nowrap;
}
.buy {
  width: 70px;
  height: 30px;
  line-height: 30px;
  border: 1px solid #e2e2e2;
  background-color: #fff;
  margin-left: 10px;
}
</style>
