<template>
  <div id="home-swiper">
    <swiper>
      <swiper-item v-for="(banner,i) in banners" :key="i">
          <a :href="banner.link">
            <img :src="banner.image">
          </a>
        </swiper-item>
    </swiper>
  </div>
</template>

<script>
import {Swiper,SwiperItem} from "components/common/swiper"
export default {
    name:"HomeSwiper",
    props:{
        banners:{
            type:Array,
            default() {
                return []
            }
        }
    },
    components:{
        Swiper,SwiperItem
    }
}
</script>

<style>

</style>