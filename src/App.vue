<template>

  <div id="app">
    <nav class="navbar navbar-static-top navbar-dark bg-inverse">
        <ul class="nav navbar-nav">
            <a class="navbar-brand" href="javascript:void(0)">Vue-UI</a>
            <li class="nav-item active"><a class="nav-link" href="/">Home</a></li>
        </ul>
    </nav>

    </img class="logo" src="./assets/logo.png">

    <nav>
        <ui-pagination page="2" row-count="150" handel-page="listenClick"></ui-pagination>
    </nav>

  </div>
</template>

<script>
import UiMessageInfo from './components/MessageInfo'
import UiPagination from './components/Pagination'

export default {
  components: {
    UiMessageInfo, UiPagination
  }
}
</script>

<style>
</style>
