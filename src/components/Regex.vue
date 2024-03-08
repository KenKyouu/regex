<script setup>
</script>
<script>
export default {
  data() {
    return{
      searchText: '',
      regexs: [
        {
          title: 'Email',
          rule: /^[A-Za-z0-9]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/,
          placeholder: '例如：aaa@aaa.com, 9527@9527.thx',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: '用戶名稱（4-16位，字母、數字、下底線、減號）',
          rule: /^[a-zA-Z0-9_-]{4,16}$/,
          placeholder: '例如：Ken123_',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: '密碼強度（至少6位，包括至少1個大寫英文字母、1個小寫英文字母、1個數字、1個特殊符號）',
          rule: /^\S*(?=\S{6,})(?=\S*\d)(?=\S*[A-Z])(?=\S*[a-z])(?=\S*[.!@#$%^&*?])\S*$/,
          placeholder: '例如：Ken123.',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: '台灣手機號碼',
          rule: /^09[0-9]{8}$/,
          placeholder: '例如：0987654321',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: '台灣身份證',
          rule: /^[a-zA-Z][1-2][0-9]{8}$/,
          placeholder: '例如：A123456789, A223456789',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: '日期（寬鬆）',
          rule: /^\d{1,4}(-)(1[0-2]|0?[1-9])\1(0?[1-9]|[1-2]\d|30|31)$/,
          placeholder: '例如：1993-08-14, 0-1-1, 0000-1-1',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: '日期（嚴謹，支援閏年）',
          rule: /^(([0-9]{3}[1-9]|[0-9]{2}[1-9][0-9]{1}|[0-9]{1}[1-9][0-9]{2}|[1-9][0-9]{3})-(((0[13578]|1[02])-(0[1-9]|[12][0-9]|3[01]))|((0[469]|11)-(0[1-9]|[12][0-9]|30))|(02-(0[1-9]|[1][0-9]|2[0-8]))))|((([0-9]{2})(0[48]|[2468][048]|[13579][26])|((0[48]|[2468][048]|[3579][26])00))-02-29)$/,
          placeholder: '例如：2024-02-29, 0001-01-01',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: '台灣各縣市',
          rule: /^台北市|臺北市|新北市|桃園市|台中市|臺中市|台南市|臺南市|高雄市|基隆市|新竹市|嘉義市|新竹縣|苗栗縣|彰化縣|南投縣|雲林縣|嘉義縣|屏東縣|宜蘭縣|花蓮縣|台東縣|臺東縣|澎湖縣|金門縣|連江縣$/,
          placeholder: '例如：桃園市',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: '24小時制時間（HH:mm:ss）',
          rule: /^(?:[01]\d|2[0-3]):[0-5]\d:[0-5]\d$/,
          placeholder: '例如：23:02:19',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: '12小時制時間（hh:mm:ss）',
          rule: /^(?:1[0-2]|0?[1-9]):[0-5]\d:[0-5]\d$/,
          placeholder: '例如：11:09:59',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: '16進位制顏色',
          rule: /^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$/,
          placeholder: '例如：#fff, #22bb33',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: '正整數，不包含0',
          rule: /^\+?[1-9]\d*$/,
          placeholder: '例如：12341',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: '負整數，不包含0',
          rule: /^-[1-9]\d*$/,
          placeholder: '例如：-12341',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: '整數',
          rule: /^(?:0|(?:-?[1-9]\d*))$/,
          placeholder: '例如：12341, 0, -12341',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: '浮點數',
          rule: /^(-?[1-9]\d*\.\d+|-?0\.\d*[1-9])$/,
          placeholder: '例如：12.341, -12.341',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: '影片連結（video），影片格式再依需求增減',
          rule: /^https?:\/\/(.+\/)+.+(\.(avi|mov|wav|mp4))$/i,
          placeholder: '例如：https://www.aaa.com/video.mp4',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: '圖片連結（image），圖片格式再依需求增減',
          rule: /^https?:\/\/(.+\/)+.+(\.(png|jpg|jpeg|svg))$/i,
          placeholder: '例如：https://www.aaa.com/image.jpg',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: 'base64格式',
          rule: /^\s*data:(?:[a-z]+\/[a-z0-9-+.]+(?:;[a-z-]+=[a-z0-9-]+)?)?(?:;base64)?,([a-z0-9!$&',()*+;=\-._~:@/?%\s]*?)\s*$/i,
          placeholder: '例如：data:image/png;base64,xxxx',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: '數字/貨幣金額（支持負數、千分位分隔號）',
          rule: /^-?\d+(,\d{3})*(\.\d{1,2})?$/,
          placeholder: '例如：1,000,000',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: '銀行卡號（16碼，寬鬆）',
          rule: /^\d{4}([\ \-]?)\d{4}\1\d{4}\1\d{4}$/,
          placeholder: '例如：1234123412341234, 1234-1234-1234-1234',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: 'VISA 銀行卡號（16碼）',
          rule: /^4\d{3}([\ \-]?)\d{4}\1\d{4}\1\d{4}$/,
          placeholder: '例如：4234123412341234, 4234-1234-1234-1234',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: 'MasterCard 銀行卡號（16碼）',
          rule: /^5[1-5]\d{2}([\ \-]?)\d{4}\1\d{4}\1\d{4}$/,
          placeholder: '例如：5134123412341234, 5134-1234-1234-1234',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: 'JCB 銀行卡號（16碼）',
          rule: /^35(?:2[89]|[3-8]\d)([\ \-]?)\d{4}\1\d{4}\1\d{4}$/,
          placeholder: '例如：3530123412341234, 3530-1234-1234-1234',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: 'American Express 銀行卡號（15碼）',
          rule: /^3[47]\d\d([\ \-]?)\d{6}\1\d{5}$/,
          placeholder: '例如：340123412341234, 3401-234567-89123',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: 'Discover Card 銀行卡號（16碼）',
          rule: /^6(?:011|22(?:1(?=[\ \-]?(?:2[6-9]|[3-9]))|[2-8]|9(?=[\ \-]?(?:[01]|2[0-5])))|4[4-9]\d|5\d\d)([\ \-]?)\d{4}\1\d{4}\1\d{4}$/,
          placeholder: '例如：6221280990124567, 6221-2809-9012-4567',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
        {
          title: 'China UnionPay 銀行卡號（16 - 19碼）',
          rule: /^62[0-5]\d{13,16}$/,
          placeholder: '例如：6212341111111111111',
          value: '',
          tagState: '',
          tagText: '驗證中...',
          copyState: '',
          copyText: '複製',
        },
      ],
    }
  },
  methods: {
    verify: function(index) {
      const regex = this.filtered[index]
      const regexRule = regex.rule
      if (regex.value == '') {
        regex.tagState = ''
        regex.tagText = '驗證中...'
      } else {
        if (new RegExp(regexRule).test(regex.value)) {
          regex.tagState = 'success'
          regex.tagText = '驗證通過'
        } else {
          regex.tagState = 'error'
          regex.tagText = '驗證不通過'
        }
      }
    },
    copy: function(index) {
      const regex = this.filtered[index]
      const regexRule = regex.rule
      navigator.clipboard.writeText(regexRule)
      regex.copyState = 'success'
      regex.copyText = '已複製!!!'
      setTimeout(() => {
        regex.copyState = ''
        regex.copyText = '複製'
      }, 1000);
    },
    clear: function(index) {
      const regex = this.filtered[index]
      regex.value = ''
      this.verify(index)
    },
  },
  computed: {
    filtered() {
      if (this.searchText) {
        return this.regexs.filter(regex => regex.title.toLowerCase().includes(this.searchText.toLowerCase()))
      } else {
        return this.regexs
      }
    }
  }
};
</script>

<template>
  <div class="search-wrap">
    <div class="container">
      <input type="text" class="regex-search" v-model="searchText" placeholder="搜尋關鍵字，如：銀行">
    </div>
  </div>
  <div class="regex-wrap">
    <div class="container">
      <div class="each-regex" v-for="(regex, index) in filtered">
        <h2 class="regex-title">{{ regex.title }}</h2>
        <div class="regex-rule">
          <button type="button" class="copy" :class="regex.copyState" @click="copy(index)">{{ regex.copyText }}</button>
          <span class="text">{{ regex.rule }}</span>
        </div>
        <div class="regex-input-wrap">
          <input type="text" class="regex-test" v-model="regex.value" :placeholder="regex.placeholder" @keyup="verify(index)">
          <button type="button" class="regex-clear" @click="clear(index)">清除</button>
        </div>
        <span class="regex-tag" :class="regex.tagState">{{ regex.tagText }}</span>
      </div>
    </div>
  </div>
</template>


<style src="../assets/css/Regex.css"/>
