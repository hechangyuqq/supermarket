<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物车</div></nav-bar>
    <scroll class="home-wrapper">
      <home-swiper :banners="banners"></home-swiper>
      <recommend-view :recommends="recommends"></recommend-view>
      <feature-view></feature-view>
      <tab-control
        :titles="['流行', '新款', '精选']"
        class="tab-control"
        @tabClick="tabClick"
      ></tab-control>
      <goods-list
        :goods="showGoods"
        class="good-list"
      ></goods-list>
    </scroll>

   
  </div>
</template>

<script>
// 外部组件
import NavBar from "components/common/navbar/NavBar";
import TabControl from "components/content/tabcontrol/TabControl.vue";
import GoodsList from "components/content/goods/GoodsList.vue";
import Scroll from 'components/common/scroll/Scroll.vue';

// 子组件
import HomeSwiper from "./childComponents/HomeSwiper";
import RecommendView from "./childComponents/RecommendView";
import FeatureView from "./childComponents/FeatureView.vue";

// 外部js文件
import { getHomeMultidata, getHomeGoods } from "network/home";



export default {
  name: "Home",
  components: {
    NavBar,
    TabControl,
    GoodsList,
    Scroll,

    HomeSwiper,
    RecommendView,
    FeatureView,


  },
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        'pop': { page: 0, list: [] },
        'new': { page: 0, list: [] },
        'sell': { page: 0, list: [] },
      },
      currentType: 'pop',
    };
  },
  created() {
    //1.网络请求相关的方法
    this.getHomeMultidata();
    this.getHomeGoods("pop");
    this.getHomeGoods("new");
    this.getHomeGoods("sell");
  },
  computed:{
    showGoods(){
      return this.goods[this.currentType].list
    }
  },
  methods: {
     /**
     * 事件监听相关的代码
      */
    tabClick(index) {
      console.log(index);
      switch (index) {
        case 0:
          this.currentType = 'pop';
          break;
        case 1:
          this.currentType = 'new';
          break;
        case 2:
          this.currentType = 'sell';
          break;
      }
    },
    //请求网络数据
    getHomeMultidata() {
      getHomeMultidata().then((res) => {
        //console.log(res)
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      });
    },
    getHomeGoods(type) {
      console.log('正在查询'+type+this.currentType)
      const page = this.goods[type].page + 1;
      getHomeGoods(type, page).then((res) => {
        this.goods[type].list.push(...res.data.list);
        this.goods[type].page += 1;
      });
    },
  },
}
</script>

<style scoped>
.home-nav {
  background-color: var(--color-tint);

  /* 设置顶部导航栏位置不变 */
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 8;
}

/* 当导航栏位置不变时，也要求轮播图显示完整  */
#home {
  padding-top: 44px;
  height: 100vh;
  position: relative;
}
.tab-control {
  position: sticky;
  top: 44px;
  z-index: 8;
}
.good-list {
  margin-bottom: 50px;
}
.home-wrapper{
  
  position:absolute;
  top: 44px;
  bottom: 49px; 
  right:0px;
  left: 0px; 
  /* height: 400px; */
  /* overflow: hidden;   */
  height: 200px;
   background-color: red;
} 
</style>
