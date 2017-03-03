<template>
  <div id="step_page">
    <div id="KV"></div>
    <img src="./assets/images/item_01.png" alt="" class="pigeon1">
    <img src="./assets/images/item_02.png" alt="" class="pigeon2">
    <img src="./assets/images/item_03.png" alt="" class="pigeon3">
    <img src="./assets/images/item_04.png" alt="" class="cloud">
    <img src="./assets/images/item_06.png" alt="" class="cloudtree">
    <img src="./assets/images/item_06.png" alt="" class="cloudtree2">
    <img src="./assets/images/item_07.png" alt="" class="cloudman">
    <img src="./assets/images/item_08.png" alt="" class="balloon1">
    <img src="./assets/images/item_09.png" alt="" class="balloon2">
    <img src="./assets/images/cloud_02.png" alt="" class="cloud3">
    <div id="step2" class="main_container">
      <div class="content">
        <div class="txt_area">
          <img src="./assets/images/indo_01.png" alt="" class="case_logo"> 
          <img src="./assets/images/indo_03.png" alt="" class="case_Q">  
          <p class="errorMsg">{{ errorMsg }}</p>
          <input type="text" name="user_family_name" v-model="familyName" class="family_name">
          <img src="./assets/images/indo_05.png" alt="" class="case_Q">
          <slick class="gift" ref="slick" :options="slickOptions">
            <div><img src="./assets/images/gift_01.png" alt=""></div>
            <div><img src="./assets/images/gift_02.png" alt=""></div>
            <div><img src="./assets/images/gift_03.png" alt=""></div>
            <div><img src="./assets/images/gift_04.png" alt=""></div>
            <div><img src="./assets/images/gift_05.png" alt=""></div>
            <div><img src="./assets/images/gift_06.png" alt=""></div>
          </slick>
          <a class="btn1" @click="next"><img src="./assets/images/btn2.gif" alt=""></a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import atui from  'atui';
import Slick from 'vue-slick';

export default {
  name: 'step-1',
  data () {
    return {
      familyName: '',
      errorMsg: '',
      status: false,
      slickOptions: {
        slidesToShow: 3,
        // Any other options that can be got from plugin documentation
      }
    }
  },
  methods: {
    rules: function () {
      console.log('test');
    },
    isChinese ( str ) {
      var regx = /[^\u4e00-\u9fa5]/;
      if(regx.test(str)) {
        return false;
      } else {
        return true;
      }
    },
    next() {
      this.$refs.slick.next();
    },

    prev() {
      this.$refs.slick.prev();
    },
  },
  watch: {
    familyName: function () {
      var self = this;
      if(self.isChinese(self.familyName)) {
        self.status = true;
        self.errorMsg = '';
      } else {
        self.status = false;
        self.errorMsg = '請輸入正確姓氏';
      }
    }
  },
  components: {
    vInput: atui.Input,
    Slick: Slick
  },
  created: function () {
  }
}
</script>

<style lang="scss">
// @import url('./assets/css/slick.css');
p.errorMsg {
  margin: 0 auto;
  text-align: center;
  color: #ff3333;
}
.slick-next:before, .slick-prev:before{
  opacity: .75;
  color: #C79A16;
}
</style>
