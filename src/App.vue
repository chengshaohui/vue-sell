<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <header-detail></header-detail>
  </div>
</template>

<script>
  import headerDetail from 'components/header-detail/header-detail'
  import qs from 'query-string'
  import {getSeller} from 'api'
  import vHeader from '@/components/v-header/v-header'

  export default {
    name: 'app',
    components: {vHeader, headerDetail},
    data () {
      return {
        seller: {
          id: qs.parse(location.search).id
        }
      }
    },
    methods: {
      _getSeller () {
        getSeller({
          id: this.seller.id
        }).then((seller) => {
          this.seller = Object.assign({}, this.seller, seller)
        })
      }
    },
    created () {
      this._getSeller()
    }
  }
</script>
<style lang="stylus"></style>
