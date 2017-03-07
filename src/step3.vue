<template>
<div id="step_page2">
  <img src="./assets/images/tree.png" alt="" class="tree">
  <img src="./assets/images/item_01.png" alt="" class="pigeon1">
  <img src="./assets/images/item_02.png" alt="" class="pigeon2">
  <img src="./assets/images/item_03.png" alt="" class="pigeon3">
  <img src="./assets/images/item_04.png" alt="" class="cloud">
  <img src="./assets/images/item_06.png" alt="" class="cloudtree">
  <img src="./assets/images/item_06.png" alt="" class="cloudtree2">
  <img src="./assets/images/item_07.png" alt="" class="cloudman">
  <img src="./assets/images/item_08.png" alt="" class="balloon1">
  <img src="./assets/images/item_09.png" alt="" class="balloon2">
  
  <!--填資料主區塊-->
  <img src="./assets/images/indo_01.png" alt="" class="case_logo_2">
  
  <div class="form">
    <img src="./assets/images/indo_09.png" alt="" class="case_Q">
    <ul>
      <li><img src="./assets/images/indo_10.png" alt=""><input name="name" v-validate data-vv-rules="required" class="input" :class="{'is-danger': errors.has('name')}" type="text" v-model="name"><span>{{ errors.first('name') }}</span></li>
      <li><img src="./assets/images/indo_11.png" alt=""><input name="tel" v-validate data-vv-rules="required|numeric" class="input" :class="{'is-danger': errors.has('tel')}" type="tel" v-model="tel"><span>{{ errors.first('tel') }}</span></li>
      <li><img src="./assets/images/indo_12.png" alt=""><input name="email" v-validate data-vv-rules="required|email" class="input" :class="{'is-danger': errors.has('email')}" type="text" placeholder="E-mail" v-model="email" /><span>{{ errors.first('email') }}</span></li>
      </li>
      <li></li>
    </ul>
    <div class="clear"></div>
    <a @click="nextStep" class="btn3 btn2"><img src="./assets/images/btn4.gif" alt=""></a>

  </div>

  <div class="memo">
    <ol>
      <li>本活動於2017/3/15起至2017/3/30止，4/10(一)將在本網站公布活動得獎名單，中獎者將由活動主辦單位透過email與簡訊通知。中獎者需至主辦單位辦公室親領，並準備身分證正反面影本，以及簽署相關勞務報酬文件。5/31(三)前未至主辦單位領取者，視同放棄中獎資格。</li>
      <li>本活動之活動辦法及相關注意事項均載明於活動網頁中，參加者於參加本活動之同時，即視為已詳閱並同意接受本活動之活動辦法及相關注意事項之規範，如有違反本活動之活動辦法及相關注意事項之行為，主辦單位得取消其參加或得獎資格外，並對於任何破壞本活動之行為保留相關權利。</li>
      <li>參加者應保證其因參加本活動所填寫或提出之資料均為真實且正確，且未冒用或盜用任何第三人之資料。一經主辦單位發現或經第三人檢舉該等資料有不實或不正確之情事，主辦單位得取消其參加或得獎資格。若因此致主辦單位無法通知其得獎訊息時，主辦單位不負任何責任，如主辦單位或其他任何第三人因此而受有損害，參加者應負一切相關責任。</li>
      <li>參加者同意並授權主辦單位將參加者於活動頁所提供之個人資料予主辦單位管理本活動使用。</li>
      <li>本活動所涉及之相關資料及記錄，均以主辦單位電腦系統所記錄或留存者為準。</li>
      <li>獎品以現金為準。如遇不可抗力之事由，主辦單位有權變更獎品內容，並改由其他等值商品取代，得獎者不得異議。且主辦單位與活動單位就該獎品不負任何維修及保固責任。
      <li>如有以下行為主辦單位有權取消參加資格，並保留相關法律追訴權利：使用不當行為或程式灌票或干擾活動進行、傳播不實謠言，造成本活動或本公司名譽受損、違反本活動辦法及政府法令之行為等。</li>
      <li>相關活動公告皆以活動網站公告為主，恕不另行通知。</li>
      <li>主辦單位保有修正、暫停或終止本活動之權利。</li>
    </ol>

  </div>

</div>
</template>

<script>
import Vue from 'vue';
import axios from  'axios';
import test from './test.js';
import config from './config.js';
import VeeValidate from 'vee-validate';
Vue.use(VeeValidate);

export default {
  name: 'step-3',
  data () {
    return {
      name: '',
      tel: '',
      email: '',
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
      self.$validator.validateAll()
      .then(result => {
        if (!result) {
          throw 'filed required.'
        }
        var params = {
          name: self.name,
          tel: self.name,
          email: self.email
        };
        return axios.post(config.rootApi+'lottery', params);
      })
      .then(function (response) {
        self.$parent.step += 1;
      })
      .catch(function (error) {
        console.warn(error);
      });
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
  components: {
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
