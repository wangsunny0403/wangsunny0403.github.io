---
title: 用Vue製作多步驟表單
categories: Vue
tags:
- Vue
- Form
# excerpt: 在Vue裡實現input輸入框字數限制，下方提示顯示輸入字元
date: 2021-11-20
# cover: '/images/vue-input-limit-cover.jpg' 
# title：文章标题
# categories：分类（最好只写一个）
# tags：标签可以多个
# excerpt：描述
# date：创建日期
# cover：缩略图（你不填就用默认的了）
---
在填寫表單時，像是問卷調查，有時候內容太過冗長，頁面看不到底不知道還有多少欄位需要填寫，這時候就可以使用「多步驟表單」來呈現了，在畫面，也可以告素使用者總共有幾個步驟需要填寫，視覺上也會比較美觀，以下用三個步驟作為範例
<h3>Step1:建立HTML</h3>
<p>先將三個步驟要呈現的內容先切出來，包含欄位及按鈕</p>
```html
<div class="form-box">
  <!--步驟1-->
  <div class="step-box">
    <div class="form-body step-box">
      <div class="form-group">
        <label for="" class="form-label">帳號</label>
        <div class="form-input-box">
          <input type="text" class="form-control" />
        </div>
      </div>
    </div>
    <div class="form-foot text-right">
      <button class="btn btn-primary">下一步</button
      >
    </div>
  </div>
  <!--步驟2-->
  <div  class="step-box">
    <div class="form-body step-box">
      <div class="form-group">
        <label for="" class="form-label">信箱</label>
        <div class="form-input-box">
          <input type="text" class="form-control" />
        </div>
      </div>
    </div>
    <div class="form-foot text-right">
      <button class="btn btn-info">上一步</button
      >
      <button class="btn btn-primary">下一步</button
      >
    </div>
  </div>
  <!--步驟3-->
  <div  class="step-box">
    <div class="form-body step-box">
      <div class="form-group">
        <label for="" class="form-label">密碼</label>
        <div class="form-input-box">
          <input type="password" class="form-control" />
        </div>
      </div>
      <div class="form-group">
        <label for="" class="form-label">確認密碼</label>
        <div class="form-input-box">
          <input type="password" class="form-control" />
        </div>
      </div>
    </div>
    <div class="form-foot text-right">
      <button class="btn btn-info">上一步</button>
      <button class="btn btn-warning">送出</button>
    </div>
  </div>
</div>
```
<div style="margin:15px 0">
  <img alt="將步驟要呈現的內容先切出來，包含欄位及按鈕" src="/images/2021-11-20-vue-form-step1.png">
</div>
<h3>Step2:用VUE，設定步驟顯示內容</h3>
設定vue程式，在data設定目前步驟為step設定為1
```javascript
data() {
  return {
    step:1, //步驟預設為第一步
  }
},
```
將html class="step-box" 設定v-if，當step = 2就會顯示該區塊內容，其他區塊就會隱藏
```html
<div class="step-box" v-if="step === 1">
  <h3 class="step-title">{{ step }}/3</h3>
</div>
<div class="step-box" v-if="step === 2">
  <h3 class="step-title">{{ step }}/3</h3>
</div>
<div class="step-box" v-if="step === 3">
  <h3 class="step-title">{{ step }}/3</h3>
</div>
```
紅框處的數字，也會提示在第幾步驟
<div style="margin:15px 0">
  <img alt="用VUE，設定步驟顯示內容" src="/images/2021-11-20-vue-form-step2.jpg">
</div>
<h3>Step3:用VUE，設定按鈕功能</h3>
再來就是在methods設定按鈕(上一步、下一步、送出按鈕)的方法，送出後，會跳出一個alert，提示送出成功
```javascript
methods:{
  prev() { //上一步按鈕
    this.step--; 
  },
  next() { //下一步按鈕
    this.step++; 
  },
  submit() { //送出按鈕
    alert('送出成功'); 
  }
}
```
```html
<button class="btn btn-info" @click="prev()">上一步</button>
<button class="btn btn-primary" @click="next()" >下一步</button>
<button class="btn btn-primary" @click="submit()" >送出</button>
```
這樣就完成了多步驟表單，以上是我的作法，如果有任何的建議或疑問，歡迎下方留言唷～
詳細程式碼：<a href="https://codepen.io/sunny0403/pen/xxLewjv" target="_blank">CodePen</a>
