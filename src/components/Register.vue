<template>
  <div id="register" class="area color-area" ref="infoBox">
    <Point :windowWidth="1898" :windowHeight="boxHeight" :draw="true" />
    <div class="wrapper">
      <div class="title">
        <h2><span>立即報</span>名</h2>
      </div>
      <div v-if="formState.active" :class="loading ? 'signup-form submit' : 'signup-form'">
        <input v-model="name" type="text" placeholder="姓名*" maxlength="50" />
        <input v-model="sex" type="text" placeholder="性別*" maxlength="5" />
        <input
          v-model="mobile"
          type="text"
          placeholder="手機*"
          maxlength="10"
          @keyup="resetMobile($event.target.value)"
        />
        <input v-model="mail" type="mail" placeholder="E-mail*" maxlength="100" />
        <!-- <input v-model="company" type="text" placeholder="公司*" maxlength="50" /> -->
        <select v-model="industry" @change="handleSelect">
          <option value="0" disabled selected>產業別*</option>
          <option value="金融保險業">金融保險業</option>
          <option value="資訊科技業">資訊科技業</option>
          <option value="服務業">服務業</option>
          <option value="專業人士(會計師、律師、醫師)">專業人士(會計師、律師、醫師)</option>
          <option value="軍.公.教">軍.公.教</option>
          <option value="家管">家管</option>
          <option value="傳播出版業">傳播出版業</option>
          <option value="製造業">製造業</option>
          <option value="學術研究">學術研究</option>
          <option value="other">其他(請說明)</option>
        </select>
        <input v-if="industry === 'other'" v-model="other" type="text" placeholder="產業別*" maxlength="20" />
        <input v-model="title" type="text" placeholder="職稱*" maxlength="50" />
        <select v-model="age">
          <option value="0" disabled selected>年齡*</option>
          <option value="35歲以下">35歲以下</option>
          <option value="36-45歲">36-45歲</option>
          <option value="46-55歲">46-55歲</option>
          <option value="56-65歲">56-65歲</option>
          <option value="65歲以上">65歲以上</option>
        </select>
        <div style="margin: 1em 0">
          <input v-model="agree" id="agree" type="checkbox" />
          <label for="agree">
            我已閱讀<mark @click.prevent="show('personalData')">個資條款</mark>且同意送出資料
          </label>
        </div>
        
        <modal
          name="personalData"
          width="90%"
          height="70%"
          @closed="closed"
        >
          <div slot="top-right">
            <button
              class="closebox"
              @click="$modal.hide('personalData')"
            >
              <i class="far fa-times-circle" />
            </button>
          </div>
          <p>謹依個人資料保護法第8條規定告知以下事項：</p>
          <p>您為本次活動的參與者(以下簡稱參與人)。參與人所填寫的資料將會提供予《今周刊》，請確認參與人在勾選同意前已詳閱並同意以下條款：《今周刊》基於客戶管理、統計及調查分析、行銷及其他合於營業登記項目或章程所定業務需要或其他法令所准許之特定目的，向參與人蒐集前述個人資料，並管理維護及處理利用。</p>
        </modal>
        <button @click="submit">確認送出</button>
      </div>

      <div v-else class="signup-form closed" v-html="formState.closeMessage" />

      <div class="alert">
        <h3>報名注意事項</h3>
        <ol>
          <li
            v-for="(list, index) in formState.alert"
            :key="index"
            v-text="list"
          />
        </ol>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Point from './Point'

export default {
  components: {
    Point
  },
  props: {
    formState: {
      type: Object,
      required: true
    }
  },
  data: function() {
    return {
      boxWidth: 0,
      boxHeight: 0,
      loading: false,
      name: null,
      sex: null,
      mobile: null,
      mail: null,
      industry: '0',
      other: null,
      title: null,
      age: '0',
      agree: false
    }
  },
  methods: {
    setViewBox () {
      this.boxWidth = this.$refs.infoBox.clientWidth;
      this.boxHeight = this.$refs.infoBox.clientHeight;
    },
    show(target) {
      this.$modal.show(target);
      const el = document.getElementsByTagName("html")[0];
      el.classList.add('fixed');
    },
    closed() {
      const el = document.getElementsByTagName("html")[0];
      el.classList.remove('fixed');
    },
    resetMobile(val) {
      this.mobile = val.replace(/\D/g, '');
    },
    handleSelect() {
      if(this.industry !== 'other') {
        this.other = null;
      }
    },
    submit() {
      if(!this.name || !this.sex || !this.mobile || !this.mail || !this.title) {
        alert('尚有欄位未填寫');
        return false;
      }
      const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      if(!pattern.test(this.mail)) {
        alert('E-mail格式錯誤');
        return false;
      }
      if(this.mobile.length < 10) {
        alert('手機號碼錯誤');
        return false;
      }
      if(this.industry === '0' || this.age === '0') {
        alert(this.industry === '0' ? '請選擇產業別' : '請選擇年齡');
        return false;
      }
      if(this.industry === 'other') {
        if(!this.other) {
          alert('請填寫產業別');
          return false;
        }
      }
      if(!this.agree) {
        alert('尚未同意個資條款');
        return false;
      }
      // 前端驗證完成 封裝送出
      this.loading = true;
      let self = this;
      axios.post('https://events.businesstoday.com.tw/event_backend/backend/happinessMatureAge2020/sign_up', {
        name: this.name,
        gender: this.sex,
        Mobile: this.mobile,
        mail: this.mail,
        category: this.industry,
        otherCategory: this.other,
        job: this.title,
        age: this.age
      })
      .then(function(response) {
        // 檢測結果
        if(response.data.status === "ok") {
          alert(self.formState.successMessage);
          self.name = null,
          self.sex = null,
          self.mobile = null,
          self.mail = null,
          self.industry = '0',
          self.other = null,
          self.title = null,
          self.age = '0',
          self.agree = false,
          self.loading = false
        } else {
          alert(`報名失敗- ${response.data.message}`);
          self.loading = false;
          console.log(response);
        }
      })
      .catch(function(error) {
        alert('報名失敗');
        self.loading = false;
        console.log(error);
      });
    }
  },
  mounted() {
    this.setViewBox();
  }
}
</script>

<style>
#register {
  text-align: center;
}
.signup-form {
  position: relative;
  width: 100%;
  max-width: 500px;
  margin: 0 auto;
  padding: 0 0 2em 0;
  text-align: center;
}
.signup-form.closed {
  background: rgba(255, 255, 255, .7);
  padding: 2em;
  margin: 2em auto;
}
.signup-form input,
.signup-form button {
  display: block;
  width: 100%;
  font-size: inherit;
  padding: 0.5em 1em;
  margin: 0.8em 0;
  border: none;
}
.signup-form input[type="checkbox"] {
  display: inline-block;
  vertical-align: middle;
  width: 1em;
  height: 1em;
  margin: 0;
}
.signup-form label {
  padding-left: 0.5em;
  display: inline-block;
  vertical-align: middle;
}
.signup-form select {
  padding: 0.5em 1em;
  margin: 0;
  font-size: 1em;
  border: none;
  width: 100%;
  background: white;
  color: #505050;
  border-radius: 0;
}
.signup-form h4 {
  text-align: left;
  font-size: 1.2em;
  font-weight: 500;
  margin: 0.4em 0;
}
.signup-form div {
  text-align: left;
  margin-bottom: 0.2em;
}
.signup-form > div:not(.vm--container) {
  white-space: nowrap;
}
.signup-form mark {
  color: #f09819;
  font-weight: 500;
  text-decoration: underline;
  padding: 0 0.2em;
  cursor: pointer;
}
.signup-form button {
  font-weight: 500;
  color: white;
  background: #f09819;
  opacity: 1;
  transition: .5s;
}
.alert {
  padding: 0 4em;
  text-align: left;
}
.alert ol li {
  list-style-type: disc;
  margin: 0.5em 0;
}
.signup-form.submit::before {
  content: '';
  position: absolute;
  width: 120%;
  height: 100%;
  top: 0;
  left: -10%;
  background: rgba(0, 0, 0, .5);
}
.signup-form.submit::after {
  content: '\f110';
  position: absolute;
  display: inline-block;
  width: 40px;
  height: 40px;
  top: 50%;
  left: 50%;
  margin: -20px 0 0 -20px;
  color: white;
  font-size: 40px;
  font-family: "Font Awesome 5 Free";
  font-weight: 900;
  font-style: normal;
  font-variant: normal;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  text-rendering: auto;
  line-height: 1;
  -webkit-animation: setRotate 2s linear infinite;
  -moz-animation: setRotate 2s linear infinite;
  animation: setRotate 2s linear infinite;
}

@media (hover: hover) {
  .signup-form > button:hover {
    opacity: .7;
  }
}

@media screen and (-ms-high-contrast: active), (-ms-high-contrast: none) {
  .signup-form > button:hover {
    opacity: .7;
  }
}

@media screen and (max-width: 1900px) {
  .signup-form {
    max-width: 420px;
  }
}

@media screen and (max-width: 1024px) {
  .signup-form {
    max-width: 360px;
  }
}

@media screen and (max-width: 640px) {
  .signup-form {
    max-width: none;
  }
  .alert {
    padding: 0.4em 0;
  }
}

@media screen and (max-width: 480px) {
  .signup-form {
    padding: 2em 2.5vw 1em;
  }
  .alert {
    padding: 0.4em 2.5vw;
  }
  .alert ol {
    padding-left: 1em;
  }
}

@media screen and (max-width: 320px) {
  .signup-form label {
    font-size: .95em;
    padding-left: 0.2em;
  }
}

</style>
