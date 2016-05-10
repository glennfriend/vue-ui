<template>
  <span class="messageInfo">
    <i v-if="icon" class="fa fa-{{this.icon}}"></i>
    <b>{{name}}</b>
    <span class="label label-default">{{value}}</span>
  </span>
</template>

<script>
export default {
  props: ['icon', 'name', 'value'],
  data () {
    return {
      abc: 'message~info~'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.messageInfo {
  margin: 5px;
}
</style>

<comment>

    <span v-if="icon">內容</span>
    -> 如果 this.icon 有值就顯示內容

</comment>

<example>
    <vui-message-info icon=""               name="Page"         value="5 / 123"></vui-message-info>
    <vui-message-info icon="database"       name="Total"        value="12,345,678"></vui-message-info>
    <vui-message-info icon="user"           name=""             value="vivian"></vui-message-info>
    <vui-message-info icon="tag"            name="tag"          value="#beauty"></vui-message-info>
    <vui-message-info icon="tags"           name="tags"         value="#beauty #nice"></vui-message-info>
    <vui-message-info icon="calendar"       name=""             value="2000-12-31"></vui-message-info>
    <vui-message-info icon="check-square-o" name=""             value="已交付"></vui-message-info>
    <vui-message-info icon="square-o"       name=""             value="未交付"></vui-message-info>
    <vui-message-info icon="envelope-o"     name="未讀取郵件"   value="12"></vui-message-info>
    <vui-message-info icon="usd"            name="price"        value="29.9900"></vui-message-info>
</example>
