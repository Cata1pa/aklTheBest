<template>
  <div>
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <swiper>
      <swiper-item v-for="(item, index) in banners">
        <a :href="item.link">
          <img :src="item.image" alt="">
        </a>
      </swiper-item>
    </swiper>
    <h2>首页</h2>
  </div>
</template>

<script>
  import NavBar from 'components/common/navbar/NavBar'
  import {Swiper, SwiperItem} from 'components/common/swiper'

  import {getMultiData, getProductData} from "network/home";

  export default {
    name: "Home",
    components: {
      NavBar,
      Swiper,
      SwiperItem
    },
    data() {
      return {
        banners: [],
        recommends: []
      }
    },
    created() {
      // 1.请求轮播等数据
      this._getMultiData()

      // 2.请求商品数据
      // this._getProductData()

      // function request(options, success, failure)
      // request({
      //   url: 'http://123.207.32.32:8000/home/data',
      //   params: {
      //     type: 'sell',
      //     page: 1
      //   }
      // }).then(res => {
      //   console.log(res);
      // }).catch(err => {
      //   console.log(err);
      // })
    //   request({
    //     url: 'http://123.207.32.32:8000/home/data',
    //     params: {
    //       type: 'sell',
    //       page: 1
    //     }
    //   }, res => {
    //     this.banners = res.data.list
    //   }, err => {
    //     console.log(err);
    //   })
    },
    methods: {
      /**
       * 网络请求
       */
      _getMultiData() {
        getMultiData().then(res => {
          this.banners = res.data.banner.list
          this.recommends = res.data.recommend.list
        })
      },
      _getProductData() {
        getProductData('sell', 1).then(res => {
          console.log(res);
        })
      }
    }
  }
</script>

<style scoped>
  .home-nav {
    background-color: var(--color-tint);
    color: #fff;
  }
</style>
