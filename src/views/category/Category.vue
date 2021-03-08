<template>
  <scroll class="home-wrapper">
              <goods-list
        :goods="showGoods"
        class="good-list"
      ></goods-list>
  ><ul>li110</ul>
  <ul>li210</ul>
  <ul>li310</ul>
  <ul>li410</ul>
  <ul>li510</ul>
  <ul>li610</ul>
  <ul>li710</ul>
  <ul>li810</ul>
  <ul>li910</ul>
  <ul>li1010</ul>
  </scroll>
</template>

<script>
import Scroll from "components/common/scroll/Scroll.vue";
import GoodsList from "components/content/goods/GoodsList.vue";
// 外部js文件
import { getHomeMultidata, getHomeGoods } from "@/network/home";
export default {
  name: "Category",
  components: { Scroll,GoodsList },
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
    methods: {
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
  overflow: hidden;  
  height: 200px;
   background-color: green;
} 
</style>
