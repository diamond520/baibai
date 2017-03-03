<template>
  <div id="home_page">
    <div id="KV"></div>
    <img src="./assets/images/emperor2.png" alt="" class="emperor3">
    <img src="./assets/images/item_01.png" alt="" class="pigeon1">
    <img src="./assets/images/item_02.png" alt="" class="pigeon2">
    <img src="./assets/images/item_03.png" alt="" class="pigeon3">
    <img src="./assets/images/item_04.png" alt="" class="cloud">
    <img src="./assets/images/item_06.png" alt="" class="cloudtree">
    <img src="./assets/images/item_07.png" alt="" class="cloudman">
    <img src="./assets/images/item_08.png" alt="" class="balloon1">
    <img src="./assets/images/item_09.png" alt="" class="balloon2">
    <img src="./assets/images/tree.png" alt="" class="tree">
    <img src="./assets/images/cloud_01.png" alt="" class="cloud2">
    <div id="home" class="main_container">
      <div class="content">
        <div class="home_txt_area">
          <p class="people_count"><span class="count_txt">目前已有</span><span class="number">{{ number }}</span><span class="count_txt">人參加遊戲！</span></p>
          <img src="./assets/images/txt.png" alt="" class="home_txt">
          <img src="./assets/images/txt2.png" alt="" class="home_txt_mobile">
          <a class="btn1" @click="next"><img src="./assets/images/btn1.gif" alt=""></a>
        </div>
        
      </div>
      
    </div>
  </div>
</template>

<script>
export default {
  name: 'home_page',
  data () {
    return {
      status: null,
      number: 0
    }
  },
  methods: {
    next: function () {
      var self = this;
      console.log(self.$parent.step);
      self.$parent.step += 1
    }
  }
}
</script>

<style lang="scss">

</style>
