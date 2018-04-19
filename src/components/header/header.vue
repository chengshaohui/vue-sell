<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar" alt="">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">{{seller.description}}/{{seller.deliveryTime}}分钟送达</div>
        <div v-if="seller.supports" class="support">
          <v-icon :classtype="seller.supports[0].type"></v-icon>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count" @click="detailShow=true">
        <span class="count">{{seller.supports.length}}个</span>
        <svg class="icon" aria-hidden="true">
          <use xlink:href="#icon-keyboard_arrow_right"></use>
        </svg>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="detailShow=true">
      <span class="bulletin-title"></span><!--
   --><span class="bulletin-text">{{seller.bulletin}}</span>
      <svg class="icon" aria-hidden="true">
        <use xlink:href="#icon-keyboard_arrow_right"></use>
      </svg>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%" alt="">
    </div>
    <transition name="fade">
      <div class="detail" v-show="detailShow">
        <div class="detail-wrapper clearfix">
          <div class="detail-main">
            <h1 class="name">{{seller.name}}</h1>
            <div class="star-wrapper">
              <star :size="48" :score="seller.score"></star>
            </div>
            <v-title v-bind:titleText="title.mes"></v-title>
            <ul v-if="seller.supports" class="supports">
              <li class="supports-item" v-for="(item, index) in seller.supports" :key="index">
                <v-icon :classtype="item.type"></v-icon>
                <span class="text">{{item.description}}</span>
              </li>
            </ul>
            <v-title v-bind:titleText="title.announcement"></v-title>
            <div class="bulletin">
              <div class="content">{{seller.bulletin}}</div>
            </div>
          </div>
        </div>
        <div class="detail-close" @click="detailShow = false">
          <svg class="icon" aria-hidden="true">
            <use xlink:href="#icon-close"></use>
          </svg>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
  import star from '../star/star'
  import vTitle from '../title/title'
  import vIcon from '../icon/icon'

  export default {
    props: {
      seller: {
        type: Object
      }
    },
    data() {
      return {
        detailShow: false,
        title: {
          mes: '优惠信息',
          announcement: '商家公告'
        }
      }
    },
    components: {
      star,
      vTitle,
      vIcon
    }
  }
</script>

<style scoped lang="scss">
  .header {
    position: relative;
    overflow: hidden;
    color: #fff;
    background-color: rgba(7, 17, 27, .5);
    .content-wrapper {
      position: relative;
      padding: 24px 12px 18px 24px;
      font-size: 0;
      .avatar {
        display: inline-block;
        vertical-align: top;
        img {
          border-radius: 2px;
        }
      }
      .content {
        display: inline-block;
        margin-left: 16px;
        .title {
          margin: 2px 0 8px 0;
          .brand {
            display: inline-block;
            vertical-align: top;
            width: 30px;
            height: 18px;
            @include bg-image('brand');
            background-size: cover;
            background-repeat: no-repeat;
          }
          .name {
            margin-left: 6px;
            font-size: 16px;
            line-height: 18px;
            font-weight: bold;
          }
        }
        .description {
          margin-bottom: 10px;
          line-height: 12px;
          font-size: 12px;
        }
        .support {
          .icon {
            width: 12px;
            height: 12px;
            margin-right: 4px;
          }
          .text {
            line-height: 12px;
            font-size: 10px;
          }
        }
      }
      .support-count {
        position: absolute;
        right: 12px;
        bottom: 14px;
        padding: 0 8px;
        height: 24px;
        line-height: 24px;
        border-radius: 14px;
        background-color: rgba(0, 0, 0, .2);
        text-align: center;
        font-size: 10px;
        .count {
          vertical-align: top;
          margin-right: 2px;
          font-size: 10px;
        }
      }
    }
    .bulletin-wrapper {
      position: relative;
      height: 28px;
      line-height: 28px;
      padding: 0 22px 0 12px;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      background-color: rgba(7, 17, 27, .2);
      .bulletin-title {
        display: inline-block;
        vertical-align: top;
        margin-top: 8px;
        width: 22px;
        height: 12px;
        @include bg-image('bulletin');
        background-size: cover;
        background-repeat: no-repeat;
      }
      .bulletin-text {
        vertical-align: top;
        font-size: 10px;
        margin: 0 4px;
      }
      .icon {
        position: absolute;
        font-size: 10px;
        right: 12px;
        top: 8px;
      }
    }
    .background {
      position: absolute;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      z-index: -1;
      filter: blur(10px);
    }
    .detail {
      position: fixed;
      top: 0;
      left: 0;
      z-index: 100;
      width: 100%;
      height: 100%;
      overflow: auto;
      background-color: rgba(7, 17, 27, .8);
      -webkit-backdrop-filter: blur(10px);
      &.fade-enter,
      &.fade-leave-to {
        opacity: 0;
        background-color: rgba(7, 17, 27, 0);
      }
      &.fade-enter-active,
      &.fade-leave-active {
        transition: all .5s;
      }
      .detail-wrapper {
        width: 100%;
        min-height: 100%;
        .detail-main {
          margin-top: 64px;
          padding-bottom: 64px;
          .name {
            line-height: 16px;
            text-align: center;
            font-size: 16px;
            font-weight: 700;
          }
          .star-wrapper {
            margin-top: 18px;
            padding: 2px 0;
            text-align: center;
          }
          .supports {
            width: 80%;
            margin: 0 auto;
            .supports-item {
              padding: 0 12px;
              margin-bottom: 12px;
              font-size: 0;
              &:last-child {
                margin-bottom: 0;
              }
              .icon {
                width: 16px;
                height: 16px;
                margin-right: 6px;
              }
              .text {
                line-height: 16px;
                font-size: 12px;
              }
            }
          }
          .bulletin {
            width: 80%;
            margin: 0 auto;
            .content {
              padding: 0 12px;
              font-size: 12px;
              line-height: 24px;
            }
          }
        }
      }
      .detail-close {
        position: relative;
        width: 32px;
        height: 32px;
        margin: -64px auto 0;
        clear: both;
        font-size: 32px;
      }
    }
  }
</style>
