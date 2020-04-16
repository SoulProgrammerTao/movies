<template>
  <div class="home">
    <div class="coming-mv">
      <p class="cm-title">即将上映</p>
      <div class="cm-box">
        <div class="cm-list">
          <div class="cm-item" v-for="(item,index) in comList" :key="index">
            <img :src="item.images.small" alt="">
            <p class="cm-name">{{item.title}}</p>
            <p class="cm-yy">主演：{{item.casts[0].name}}</p>
            <p class="cm-yy">{{item.mainland_pubdate}}</p>
          </div>
        </div>
      </div>
    </div>
    <div class="hot-mv">
      <p class="hot-title">正在热映</p>
      <div class="hot-list">
        <div class="hot-item" v-for="(item,index) in hotList" :key="index">
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
          <button class="buy" @click="goDetail(item)">想看</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data () {
    return {
      hotList: [],
      comList: []
    }
  },

  components: {
  },
  beforeMount() {
    wx.getStorage({
      key: 'hotList',
      success: (res) => {
        this.hotList = res.data
      },
      fail: () => {
        this.getHotList()
      }
    })
    wx.getStorage({
      key: 'comList',
      success: (res) => {
        this.comList = res.data
      },
      fail: () => {
        this.getComList()
      }
    })
  },
  methods: {
    getHotList () {
      //获取豆瓣电影的电影列表信息
      wx.request({
        url: 'https://douban.uieee.com/v2/movie/in_theaters',
        method:'GET',
        header:{
          "Content-Type":"json"
        },
        success: (res) => {
          this.hotList = res.data.subjects
          wx.setStorage({
            key: "hotList",
            data: this.hotList
          })
        }
      })
    },
    getComList () {
      //获取豆瓣电影的电影列表信息
      wx.request({
        url: 'https://douban.uieee.com/v2/movie/coming_soon',
        method:'GET',
        header:{
          "Content-Type":"json"
        },
        success:(res) => {
          this.comList = res.data.subjects
          wx.setStorage({
            key: "comList",
            data: this.comList
          })
        }
      })

    },
    goDetail (item) {
      wx.setStorage({
        key: "detail",
        data: item
      })
      wx.navigateTo({
        url: `/pages/detail/main`
      })
    }
  },

  created () {
  }
}
</script>

<style scoped>
.home {
  width: 100%;
  overflow-x: hidden;
  background-color: #f5f5f5;
}
.coming-mv {
  background-color: #fff;
  padding-bottom: 20px;
  border-bottom: 1px solid #e2e2e2;
}
.cm-title {
  padding: 10px;
}
.cm-box {
  padding-left: 10px;
  width: 100%;
  overflow-x: auto;
}
.cm-list {
  width: auto;
  white-space: nowrap;
}
.cm-item {
  width: 100px;
  display: inline-block;
  margin-right: 10px;
}
.cm-item>img {
  width: 100%;
  height: 135px;
}
.cm-name {
  font-size: 15px;
}
.cm-yy {
  font-size: 14px;
  color: #999;
  white-space: nowrap;
}
.hot-mv {
  margin-top: 10px;
  background-color: #fff;
  border-top: 1px solid #e2e2e2;
}
.hot-title {
  padding-left: 10px;
  padding-top: 10px;
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
