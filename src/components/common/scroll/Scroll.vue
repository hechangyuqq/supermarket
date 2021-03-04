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
      }
    };
  },
  mounted() {
    this.$nextTick(()=>{
          this.scroller = new BScroll(this.$refs.wrapper, {
      // probeType:this.probeType,
      //probeType: 3,
      scrollY: true,
      click: true,
      mouseWheel: true,
      //pullUpLoad: true
    });
    // console.log( "hasVerticalScroll:"+this.scroller.hasVerticalScroll);
    // console.log( "scrollerHeight:"+this.scroller.scrollerHeight);
    // console.log( "wrapperHeight:"+this.scroller.wrapper.wrapperHeight);
    console.log(this.scroller)
    })

  }
}
</script>

<style></style>
