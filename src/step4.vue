<template>
  <div id="step_page2" class="end_page">

    <img src="./assets/images/emperor2.png" alt="" class="emperor2">
    <img src="./assets/images/tree.png" alt="" class="tree">
    <img src="./assets/images/item_01.png" alt="" class="pigeon1">
    <img src="./assets/images/item_02.png" alt="" class="pigeon2">
    <img src="./assets/images/item_03.png" alt="" class="pigeon3">
    <img src="./assets/images/cloud_01.png" alt="" class="cloud2">
    <img src="./assets/images/cloud_02.png" alt="" class="cloud3">
    <img src="./assets/images/cloud_03.png" alt="" class="cloud4">
    <img src="./assets/images/item_06.png" alt="" class="cloudtree">
    <img src="./assets/images/item_06.png" alt="" class="cloudtree2">
    <img src="./assets/images/item_07.png" alt="" class="cloudman2">
    <img src="./assets/images/item_08.png" alt="" class="balloon1">
    <img src="./assets/images/item_09.png" alt="" class="balloon2">
    
    <img src="./assets/images/indo_01.png" alt="" class="case_logo_2">
    <!-- Line 分享按鈕 -->
    <div class="line">
      <a id="Linemobile" class="shareBtn mobile" href="http://line.naver.jp/R/msg/text/?黃帝拜祖 萬姓開示 http://URL" target="_blank"></a>  
      <a id="LinePc" class="shareBtn pc" href="http://line.naver.jp/R/msg/text/?黃帝拜祖 萬姓開示 http://URL" target="_blank"></a>  
    </div>
    <img src="./assets/images/indo_02.png" alt="" class="end_info">
    <img src="./assets/images/indo_04.png" alt="" class="end_info last_info">

  </div>
</template>

<script>
import atui from  'atui';
import test from './test.js';

export default {
  name: 'step-3',
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
    nextStep: function () {
      var self = this;
      self.$parent.step += 1;
      console.log(self.$parent.result);
      // console.log( self.pickRandomProperty( test.elegant) );
      return;
      // console.log(self.$parent.step);
      // console.log(this.$refs.slick.$el.slick.currentSlide)
      // this.currentSlide = $('.gift')[0].slick.currentSlide;
      // this.currentSlide = this.$refs.slick.$el.slick.currentSlide;
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
