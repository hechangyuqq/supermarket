<template>
  <div class="TabControl">
    <div v-for="(title,index) in titles" 
    class="tab-control-item" 
    :key="index" 
    :class="{active : index === currentIndex}"
    @click="tabClick(index)">
      <span>{{title}}</span>
    </div>
 

  </div>
   
</template>

<script>
export default {
    name:"TabControl",
    props:{
      titles:{
        type:Array,
        default(){
          return []
        }
      }
    },
    data(){
      return {
        currentIndex:0,
      }
    },
    methods : {
      tabClick(index){
        this.currentIndex = index;  
        this.$emit('tabClick',index);
      }
    }
}
</script>

<style>
.TabControl {
  display: flex;
  font-size: 18px;
  text-align: center;
  padding: 8px;
  background-color: white;
}

.tab-control-item {
  flex: 1;
}
/* 对所有span设置padding */
.tab-control-item span {
  padding: 5px;
}
.active {
  color: var(--color-high-text);
}
/* 被选中时的那一个span标签的颜色设置，只对选中的那一个span */
.active span {
  border-bottom: 3px solid var(--color-tint);
}

</style>