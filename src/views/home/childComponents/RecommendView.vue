<template>
  <div class="home-recommend" >
      <div class="image-item" v-for= "recommend in recommends" :key="recommend.title">
          <a :href="recommend.link">
              <img :src="recommend.image">
              <div>{{recommend.title}}</div>
          </a>
      </div>
  </div>
</template>

<script>
export default {
    name:"RecommendView",
    props:{
        recommends:{
            type:Array,
            default(){
                return []
            }
        }
    }
}
</script>

<style>
/* github有很多后台管理系统 */
.home-recommend {
    
    /* 弹性布局 */
    display: flex;
    /* 宽度铺满屏幕 */
    width:100%;
    /* 图片和文字居中 */
    text-align : center;
    font-size: 12px;

/* 间距和底部阴影 */
    padding: 10px 0 10px;
    border-bottom: 8px solid #eee;
}
.image-item {
    /* 保证每个元素均分 */
    flex:1;

}

.home-recommend img {
    width: 70px;
    height: 70px;
    margin-bottom: 5px;
}
</style>