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
          <a class="btn1" @click="nextStep"><img src="./assets/images/btn2.gif" alt=""></a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import atui from  'atui';
import Slick from 'vue-slick';
// import $ from 'jquery';
import test from './test.js';

export default {
  name: 'step-1',
  data () {
    return {
      familyName: '',
      errorMsg: '',
      status: false,
      slickOptions: {
        slidesToShow: 1,
        initialSlide: 0
      },
      currentSlide: 0,
      oblation: ['flower','eaten','wine','fruit','bao','incense'],
      result: {
        oblation: "",
        familyName: ""
      }
    }
  },
  methods: {
    rules: function () {
      console.log('test');
    },
    isChinese ( str ) {
      var self = this
      var regx = /[^\u4e00-\u9fa5]/;
      if(!str){ 
        return false;
      }
      if(regx.test(str)) {
        return false;
      } else {
        return true;
      }
    },
    nextStep: function () {
      var self = this;
      if(!self.status){ 
        console.warn('family name invalid.');
        return;
      }
      this.currentSlide = this.$refs.slick.$el.slick.currentSlide;
      self.$parent.result = {
        oblation : self.oblation[this.currentSlide],
        familyName: self.familyName
      }
      self.$parent.step += 1;
      return;
    },
    next() {
      var self = this;
      self.$refs.slick.next();
    },
    prev() {
      var self = this;
      self.$refs.slick.prev();
    },
    pickRandomProperty: function (obj) {
        var result;
        var count = 0;
        for (var prop in obj)
          if (Math.random() < 1/++count)
            result = prop;
        return result;
    }
  },
  watch: {
    familyName: function (familyName) {
      var self = this;
      if(self.isChinese(familyName)) {
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
.slick-slide img {
  margin: 0 auto;
}
.form li {
  text-align: center;
  span {
    color: #ff3333;
  }
}
.input.is-danger, .textarea.is-danger {
  border-color: #ff3860;
  border: 1px solid #ff3860;
  border-radius: 3px;
}
</style>
