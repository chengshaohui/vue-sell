<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
  </div>
</template>

<script>
  import qs from 'query-string'
  import {getSeller} from 'api'
  import vHeader from '@/components/v-header/v-header'

  export default {
    name: 'app',
    components: {vHeader},
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
