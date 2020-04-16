<template>
  <div class="search">
    <div class="sh-input">
      <input type="text" v-model="q" placeholder="请输入您要搜索的电影">
      <div class="btn" @click="getMvList">
        <img src="../../../static/images/sousuo.png" alt="">
      </div>
    </div>
    <div class="hot-list">
      <div class="hot-item" v-for="(item,index) in mvList" :key="index">
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
        <button class="buy">购票</button>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  data () {
    return {
      q: null,
      mvList: []

    }
  },
  methods: {
    getMvList () {
      //获取豆瓣电影的电影列表信息
      wx.request({
        url: `https://douban.uieee.com/v2/movie/search?q=${this.q}`,
        method:'GET',
        params: {
          q: this.q
        },
        header:{
          "Content-Type":"json"
        },
        success: (res) => {
          this.mvList = res.data.subjects
        }
      })
    }
  }
}
</script>

<style>
.search {
}
.sh-input {
  height: 50px;
  border-bottom: 1px solid #e2e2e2;
  border-top: 1px solid #e2e2e2;
  display: flex;
  align-items: center;
}
.sh-input > input {
  flex: 1;
  height: 30px;
  padding-left: 10px;
}
.sh-input > .btn {
  width: 50px;
  height: 50px;
  border-left: 1px solid #e2e2e2;
  display: flex;
  justify-content: center;
  align-items: center;
}
.sh-input > .btn > img {
  width: 30px;
  height: 30px;
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
