<template>
  <div id="step_page">

    <div id="KV">
      <img src="./assets/images/fruit.png" alt="" class="chosen_gift">
    </div>
    
    <img src="./assets/images/item_01.png" alt="" class="pigeon1">
    <img src="./assets/images/item_02.png" alt="" class="pigeon2">
    <img src="./assets/images/item_03.png" alt="" class="pigeon3">
    <img src="./assets/images/item_04.png" alt="" class="cloud">
    <img src="./assets/images/item_06.png" alt="" class="cloudtree">
    <img src="./assets/images/item_06.png" alt="" class="cloudtree2">
    <img src="./assets/images/item_07.png" alt="" class="cloudman">
    <img src="./assets/images/item_08.png" alt="" class="balloon1">
    <img src="./assets/images/item_09.png" alt="" class="balloon2">

    <div id="step2" class="main_container">
      <div class="content">
        <div class="txt_area">
          <img src="./assets/images/indo_01.png" alt="" class="case_logo">
          <img src="./assets/images/indo_06.png" alt="" class="case_Q">
          <div class="emperor_gift">
            <img src="./assets/images/emperor2.png" alt="" class="emperor3"> 
            <img v-if="oblation == 'wine'" src="./assets/images/wine.png" alt="" class="chosen_gift2">
            <img v-if="oblation == 'eaten'" src="./assets/images/eaten.png" alt="" class="chosen_gift2">
            <img v-if="oblation == 'flower'" src="./assets/images/flower.png" alt="" class="chosen_gift2">
            <img v-if="oblation == 'bao'" src="./assets/images/bao.png" alt="" class="chosen_gift2">
            <img v-if="oblation == 'incense'" src="./assets/images/incense.png" alt="" class="chosen_gift2">
          </div>
          
          <p class="man">{{ elegant }}</p>
          <div class="clear"></div>

          <p class="result">
            <span class="who">選擇{{ oblationChn[oblation] }}者</span>
            <span v-html="oblationHtml"></span>
          </p>
          <a @click="nextStep" class="btn1 btn2"><img src="./assets/images/btn3.gif" alt=""></a>
        </div>
          
        
      </div>
      
    </div>
  </div>
</template>

<script>
import atui from  'atui';
import test from './test.js';

export default {
  name: 'step-2',
  data () {
    return {
      elegant: '',
      oblation: '',
      imgUrl: '',
      oblationHtml: '',
      oblationChn: {
        'flower': "鮮花",
        'eaten': "三牲",
        'wine': "米酒",
        'fruit': "水果",
        'bao': "壽桃",
        'incense': "香燭"
      },
      errorMsg: '',
      status: false,
      slickOptions: {
        slidesToShow: 1,
        initialSlide: 0
      },
      currentSlide: 0
    }
  },
  methods: {
    rules: function () {
      // console.log('test');
    },
    isChinese ( str ) {
      var regx = /[^\u4e00-\u9fa5]/;
      if(regx.test(str)) {
        return false;
      } else {
        return true;
      }
    },
    nextStep: function () {
      var self = this;
      self.$parent.step += 1;
      return;
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
  },
  created: function () {
    var self = this;
    self.elegant = test.elegant[self.$parent.result.familyName] || this.pickRandomProperty(test.elegant);
    self.oblation = self.$parent.result.oblation;
    self.imgUrl = './images/'+self.oblation+'.png';
    self.oblationHtml = test.oblation[self.oblationChn[self.oblation]];
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
</style>
