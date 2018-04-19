<template>
  <span class="icon" :class="classMap[classtype]"></span>
</template>

<script>
  export default {
    name: 'icon',
    props: {
      classtype: {
        type: Number
      }
    },
    created() {
      this.classMap = ['decrease', 'discount', 'guarantee', 'invaice', 'special']
    }
  }
</script>

<style scoped lang="scss">
  @import '../../common/scss/mixin.scss';
  .icon {
    display: inline-block;
    vertical-align: top;
    background-repeat: no-repeat;
    background-size: cover;
    &.decrease {
      @include bg-image('decrease_3');
    }
    &.discount {
      @include bg-image('discount_3');
    }
    &.guarantee {
      @include bg-image('guarantee_3');
    }
    &.invaice {
      @include bg-image('invoice_3');
    }
    &.special {
      @include bg-image('special_3')
    }
  }
</style>
