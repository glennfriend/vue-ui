<template>
  <ul class="pagination" v-if="isShow">

    <li v-bind:class="['page-item', {disabled: page <= 1}]"
        v-on:click="eventPage('first')">
        <a href="javascript:void(0)" class="page-link">
            <span>{{showFirst}}</span>
        </a>
    </li>

    <li v-bind:class="['page-item', {disabled: page <= 1}]"
        v-on:click="eventPage('prev')">
        <a href="javascript:void(0)" class="page-link">
            <span>{{showPrev}}</span>
        </a>
    </li>

<!--
    <li class="page-item active" v-if="page == index"
        v-for="index in getShowPages()">
      [<a href="javascript:void(0)" class="page-link">{{index}}</a>]
    </li>

    <li class="page-item" v-if="page != index"
        v-for="index in getShowPages()"
        v-on:click="eventPage(index)">
      <a href="javascript:void(0)" class="page-link">{{index}}</a>
    </li>
-->

    <li v-bind:class="['page-item', {active: page==index}]"
        v-for="index in getShowPages()"
        v-on:click="eventPage(index)">

      <a href="javascript:void(0)" class="page-link">{{index}}</a>

    </li>

<!--
    <li v-bind:class="['page-item', {active: page==index}]"
        v-for="index in getShowPages()"
        v-on:click="eventPage(index)">

      <a href="javascript:void(0)" class="page-link">{{index}}</a>

    </li>
-->
    <li v-bind:class="['page-item', {disabled: page >= getTotalPage()}]"
        v-on:click="eventPage('next')">
        <a href="javascript:void(0)" class="page-link">
            <span>{{showNext}}</span>
        </a>
    </li>

    <li v-bind:class="['page-item', {disabled: page >= getTotalPage()}]"
        v-on:click="eventPage('last')">
        <a href="javascript:void(0)" class="page-link">
            <span>{{showLast}}</span>
        </a>
    </li>

  </ul>
</template>

<script>
export default {
  props: [
    'page', 'rowCount', 'handelPage'
  ],
  data () {
    this.isShow = false
    this.showPrev = '‹ Prev'
    this.showNext = 'Next ›'
    this.showFirst = '«'
    this.showLast = '»'
    this.pageShowCount = 15     // 預設值為每頁 15 筆
    this.gap = 5                // 顯示多少可點擊頁數  << < 1 2 3 4 5 > >>
    // this.rowCount = 0        // 總筆數
    this.page = this.page ? this.page : 1
    if (!this.rowCount || this.rowCount <= 0) {
      this.rowCount = 0
    }
    if (this.rowCount > 0) {
      this.isShow = true
    }
    return {}
  },
  methods: {

    /**
     *  計算總頁數
     */
    getTotalPage: function () {
      return Math.ceil(this.rowCount / this.pageShowCount)
    },

    /**
     *  取得要顯示哪幾頁 page
     *      example:
     *          [5,6,7,8,9]
     *
     *  @return array
     */
    getShowPages: function () {
      let total = this.getTotalPage()
      let start, stop
      if (total >= this.gap) {
        // 顯示 gap 的數量
        // 必須要計算 active page 在中間的位置
        start = this.page - Math.floor(this.gap / 2)
        if (start < 1) {
          start = 1
        }
        stop = start + this.gap - 1
        if (stop > total) {
          stop = total
          start = total - this.gap + 1  // 開始的頁數要回補, 不然在尾頁的數量會少於 gap
        }
      } else {
        // 顯示間距若少於 gap, 那麼就都顯示
        start = 1
        stop = total
      }

      let arr = []
      let index = 0
      for (let i = start; i <= stop; i++) {
        arr[index++] = i
      }
      return arr
    },

    /**
     *  點擊
     */
    eventPage: function (pageType) {
      var page
      switch (pageType) {
        case 'first':
          page = 1
          break
        case 'prev':
          page = parseInt(this.page, 10) - 1
          break
        case 'next':
          page = parseInt(this.page, 10) + 1
          break
        case 'last':
          page = this.getTotalPage()
          break
        default:
          page = parseInt(pageType, 10)
          break
      }

      if (page > this.getTotalPage()) {
        page = this.getTotalPage()
      }
      if (page <= 0) {
        page = 1
      }

      console.log(page)
      console.log(this.page)
      if (page !== this.page && this.handelPage) {
        this.handelPage(page)
      }
    }

  }
}
</script>

<!-- in "scoped" -->
<style scoped>
</style>

<example>
    <nav>
        <ui-pagination page="2" row-count="150"></ui-pagination>
    </nav>
</example>