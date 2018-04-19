<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <ul class="tab border-1px">
      <li class="tab-item">
        <router-link to="goods" exact>商品</router-link>
      </li>
      <li class="tab-item">
        <router-link to="ratings" exact>评论</router-link>
      </li>
      <li class="tab-item">
        <router-link to="seller" exact>商家</router-link>
      </li>
    </ul>
    <router-view :seller="seller"></router-view>
  </div>
</template>

<script>
  import Header from './components/header/header.vue'
  import './common/fonts/iconfont'

  const ERR_OK = 0
  export default {
    name: 'APP',
    data() {
      return {
        seller: {}
      }
    },
    created() {
      this.$http.get('./api/seller').then(res => {
        res = res.body
        if (res.errno === ERR_OK) {
          this.seller = res.data
        }
      })
    },
    components: {
      'v-header': Header
    }
  }
</script>

<style lang="scss">
  .icon {
    width: 1em;
    height: 1em;
    vertical-align: -0.15em;
    fill: currentColor;
    overflow: hidden;
  }
  #app {
    .tab {
      display: flex;
      width: 100%;
      height: 40px;
      line-height: 40px;
      @include bottom-1px(rgba(7, 17, 27, .1));
      .tab-item {
        flex: 1;
        text-align: center;
        a {
          font-size: 14px;
          color: rgb(77, 85, 93);
        }
        a.active {
          color: rgb(240, 20, 20);
        }
      }
    }
  }
</style>
