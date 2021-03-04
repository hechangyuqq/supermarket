<template>
  <div id="app">
    <main-tab-bar class="main-tab-bar"></main-tab-bar>
    <router-view></router-view>
  </div>
</template>

<script>

 import MainTabBar from 'components/content/maintabbar/MainTabBar.vue'

export default {
  name: 'App',
  components: {
     MainTabBar,
  }
}
</script>

<style>

 @import  'assets/css/base.css';
 /* html,body,#app{
  height: 100%;
} */
.main-tab-bar{
  z-index: 9;
}
</style>
