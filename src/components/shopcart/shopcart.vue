<template>
  <div class="shopcart">
    <div class="content">
      <div class="content-left">
        <div class="logo-wrapper">
          <div class="logo" :class="{highlight: totalCount > 0}">
            <svg class="icon" :class="{highlight: totalCount > 0}" aria-hidden="true">
              <use xlink:href="#icon-shopping_cart"></use>
            </svg>
          </div>
          <div class="num" v-show="totalCount > 0">{{totalCount}}</div>
        </div>
        <div class="price" :class="{highlight: totalPrice > 0}">￥{{totalPrice}}</div>
        <div class="description">另需配送费￥{{deliveryPrice}}元</div>
      </div>
      <div class="content-right">
        <div class="pay" :class="payClass">
          <span class="pay-desc">{{payDesc}}</span>
        </div>
      </div>
    </div>
    <div class="ball-container">
      <transition name="drop">
        <div v-for="ball in balls" v-show="ball.show">
          <div class="inner"></div>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'shopcart',
    props: {
      deliveryPrice: {
        type: Number,
        default: 0
      },
      minPrice: {
        type: Number,
        default: 0
      },
      selectFoods: {
        type: Array,
        default() {
          return [
            {price: 30, count: 2}
          ]
        }
      }
    },
    data() {
      return {
        balls: [
          {show: false},
          {show: false},
          {show: false},
          {show: false},
          {show: false}
        ]
      }
    },
    computed: {
      totalPrice() {
        let total = 0
        this.selectFoods.forEach(food => {
          total += food.price * food.count
        })
        return total
      },
      totalCount() {
        let count = 0
        this.selectFoods.forEach(food => {
          count += food.count
        })
        return count
      },
      payDesc() {
        if (this.totalPrice === 0) {
          return `￥${this.minPrice}元起送`
        } else if (this.totalPrice < this.minPrice) {
          let diff = this.minPrice - this.totalPrice
          return `还差￥${diff}元起送`
        } else {
          return '去结算'
        }
      },
      payClass() {
        if (this.totalPrice < this.minPrice) {
          return 'not-enough'
        } else {
          return 'enough'
        }
      }
    }
  }
</script>

<style scoped lang="scss">
  .shopcart {
    position: fixed;
    left: 0;
    bottom: 0;
    z-index: 50;
    width: 100%;
    height: 48px;
    .content {
      display: flex;
      height: 100%;
      color: rgba(255, 255, 255, .4);
      background-color: #141d27;
      .content-left {
        display: flex;
        align-items: center;
        flex-grow: 1;
        font-size: 0;
        .logo-wrapper {
          display: inline-block;
          position: relative;
          top: -5px;
          margin: 0 12px;
          padding: 6px;
          width: 56px;
          height: 56px;
          box-sizing: border-box;
          border-radius: 50%;
          background-color: #141d27;
          .logo {
            display: flex;
            justify-content: center;
            align-items: center;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            background-color: #2b343c;
            &.highlight {
              background-color: rgb(0, 160, 220);
            }
            .icon {
              font-size: 24px;
              color: rgba(255, 255, 255, .4);
              &.highlight {
                color: #fff;
              }
            }
          }
          .num {
            position: absolute;
            top: 0;
            right: 0;
            width: 24px;
            height: 16px;
            line-height: 16px;
            text-align: center;
            border-radius: 16px;
            font-size: 9px;
            font-weight: 700;
            color: #fff;
            background-color: rgb(240, 20, 20);
            box-shadow: 0 4px 8px 0 rgba(0, 0, 0, .4);
          }
        }
        .price {
          line-height: 24px;
          height: 24px;
          box-sizing: border-box;
          padding-right: 12px;
          border-right: 1px solid rgba(255, 255, 255, .1);
          font-size: 16px;
          font-weight: 700;
          &.highlight {
            color: #fff;
          }
        }
        .description {
          padding-left: 12px;
          font-size: 12px;
        }
      }
      .content-right {
        display: flex;
        flex: 0 0 105px;
        width: 105px;
        height: 100%;
        justify-content: center;
        align-items: center;
        background-color: #2B333B;
        .pay {
          display: flex;
          width: 100%;
          height: 100%;
          font-size: 12px;
          font-weight: 700;
          .pay-desc {
            margin: auto;
          }
          &.not-enough {
            background-color: #2b333b;
          }
          &.enough {
            background-color: #00b43c;
            color: #fff;
          }
        }
      }
    }
    .ball-container {
      .ball {
        position: fixed;
        left: 32px;
        bottom: 22px;
        z-index: 200;
        &.drop-enter-active {
          transition: all .4s;
          .inner {
            width: 16px;
            height: 16px;
            border-radius: 50%;
            background: rgb(0, 160, 220);
            transition: all .4s;
          }
        }
      }
    }
  }
</style>
