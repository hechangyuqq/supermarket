<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from "better-scroll";
export default {
  name: "Scroll",
  data() {
    return {
      scroller: {
        type: Object,
        default() {
          return {};
        }
      },

    };
  },
  props: {
    probeType: {
      type: Number,
      default: 0
    },
    pullUpLoad:{
      type:Boolean,
      default:false
    }
  },
  mounted() {
    this.scroller = new BScroll(this.$refs.wrapper, {
      // probeType:this.probeType,
      probeType: this.probeType,
      click: true,
      mouseWheel: true,
      pullUpLoad:this.pullUpLoad,
      //pullUpLoad: true
    })
    if( this.probeType === 2 || this.probeType===3){
      this.scroller.on("scroll", (position) => {
      // console.log(position);
      this.$emit('scroll',position)
    })
    }

    if (this.pullUpLoad){
      this.scroller.on("pullingUp",() => {
        //console.log('上拉加载更多')
        this.$emit('pullingUp')
      })      
    }

    // console.log( "hasVerticalScroll:"+this.scroller.hasVerticalScroll);
    // console.log( "scrollerHeight:"+this.rscroller.scrollerHeight);
    // console.log( "wrapperHeight:"+this.scoller.wrapper.wrapperHeight);
  },
  methods: {
    scrollTo(x, y, time) {
      this.scroller && this.scroller.scrollTo(x, y, time);
    },
    finishPullUp(){
      this.scroller.finishPullUp()
    },
    refresh(){
      //console.log('----------')
      this.scroller && this.scroller.refresh();
    },

  }
};
</script>

<style></style>
