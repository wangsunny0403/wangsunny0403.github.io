---
title: 用Vue製作拖拽排序
categories: Vue
tags:
- Vue
- Vue3
# excerpt: 在Vue裡實現input輸入框字數限制，下方提示顯示輸入字元
date: 2021-11-25
# cover: '/images/vue-input-limit-cover.jpg' 
# title：文章标题
# categories：分类（最好只写一个）
# tags：标签可以多个
# excerpt：描述
# date：创建日期
# cover：缩略图（你不填就用默认的了）
---
在製作管理端時，很常遇到需要排序的功能，以下要介紹使用「vue-draggable-next」套件製作拖曳排序功能。
<div style="margin:15px 0">
  <img alt="用Vue製作拖拽排序" src="/images/2021-11-25-vue-drag-and-drop.png">
</div>
<h3>Step1:先安裝「vue-draggable-next」套件</h3>
```javascript
npm install vue-draggable-next
//or
yarn add vue-draggable-next
```
<h3>Step2:分別在HTML、CSS樣式及Script新增程式碼</h3>
<p>以下是使用手刻表格製作，icon是用fontawesome</p>
<h4>html</h4>
```html
<div class="div-table text-center">
  <div class="thead">
    <div class="tr">
      <div class="th width-80">調整</div>
      <div class="width-80 th">顯示順位</div>
      <div class="th">名稱</div>
    </div>
  </div>
  <div class="tbody">
    <div class="tr" v-for="(element, index) in list" :key="element.name">
      <div class="width-80 td table-move">
        <i class="fas fa-arrows-alt"></i>
      </div>
      <div class="width-80 td">
        {{ index + 1 }}
      </div>
      <div class="td">{{ element.name }}</div>
    </div>
  </div>
</div>
<!-- end div-table -->
```
Tips:顯示順位欄位是能讓使用者清楚知道排序順序
<h4>Script</h4>
<p>加入列表動態資料</p>
```javascript
import { ref } from 'vue';
export default {
  setup() {
    const list = ref([
      {
        name: '名稱1',
      },
      {
        name: '名稱2',
      },
      {
        name: '名稱3',
      },
      {
        name: '名稱4',
      },
    ]);
    return {
      list,
    };
  },
};
```
<h4>SCSS樣式</h4>
```css
.div-table {
  display: table;
  width: 100%;
  .thead {
    display: table-header-group;
  }
  .tbody {
    display: table-row-group;
  }
  .tr {
    display: table-row;
    &:nth-child(2n + 2) {
      .td {
        background-color: #fafafa;
      }
    }
  }
  .th,
  .td {
    display: table-cell;
    vertical-align: middle;
    padding: 0.5rem;
    white-space: nowrap;
  }
  .th {
    background-color: #293042;
    color: $white;
  }
  .td {
    border-bottom: 1px solid #dcdfe6;
  }
}
```
<h3>Step3:在table加入vue-draggable-next套件</h3>
<h4>Script</h4>
<p>在script import vue-draggable-next套件</p>
```javascript
import { VueDraggableNext } from 'vue-draggable-next';
export default {
  //加入vue-draggable-next components
  components: {
    draggable: VueDraggableNext,
  },
};
```
<h4>Step4:在html加入draggable元件</h4>
<p>將< div class="tbody" :list="list">< /div>改為< draggable class="tbody" :list="list">< /draggable><br/>
(這裡會這樣改是因為樣式排版的關係，依照個人樣式設定做調整，不影響拖曳效果)</p>
```html
<draggable class="tbody" :list="list">
  <div class="tr" v-for="(element, index) in list" :key="element.name">
    <div class="width-80 td table-move">
      <i class="fas fa-arrows-alt"></i>
    </div>
    <div class="width-80 td">
      {{ index + 1 }}
    </div>
    <div class="td">{{ element.name }}</div>
  </div>
</draggable>
```
<h3>完整的程式碼</h3>
```html
<div class="div-table text-center">
  <div class="thead">
    <div class="tr">
      <div class="th width-80">調整</div>
      <div class="width-80 th">顯示順位</div>
      <div class="th">名稱</div>
    </div>
  </div>
  <draggable class="tbody" :list="list">
    <div class="tr" v-for="(element, index) in list" :key="element.name">
      <div class="width-80 td table-move">
        <i class="fas fa-arrows-alt"></i>
      </div>
      <div class="width-80 td">
        {{ index + 1 }}
      </div>
      <div class="td">{{ element.name }}</div>
    </div>
  </draggable>
</div>
<!-- end div-table -->
```
```javascript
<script>
import { VueDraggableNext } from 'vue-draggable-next';
import { ref } from 'vue';
export default {
  components: {
    draggable: VueDraggableNext,
  },
  setup() {
    const list = ref([
      {
        name: '名稱1',
        id: 1,
        link: '開幕慶活動',
        cover: 'yes',
        type: 'active',
      },
      {
        name: '名稱2',
        id: 2,
        link: 'https://www.google.com/',
        cover: '',
        type: 'self',
      },
      {
        name: '名稱3',
        id: 3,
        link: 'https://www.facebook.com/',
        cover: '',
        type: 'self',
      },
      {
        name: '名稱4',
        id: 4,
        link: 'https://www.facebook.com/',
        cover: '',
        type: 'self',
      },
    ]);
    return {
      list,
    };
  },
};
</script>
```
<p>這樣就完成了拖曳排序的功能囉～完整套件資訊可以到官方<a href="https://github.com/anish2690/vue-draggable-next" target="_blank">Github</a>查看</p>
<p>以上是我的作法，如果有任何的建議或疑問，歡迎下方留言唷～</p>
