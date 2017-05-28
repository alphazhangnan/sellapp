<template>
<transition name="move">
  <div class="detailWrapper" ref="detailWrapper" v-show="showDetail">
    <div class="foodDetail">
      <div class="image-header">
        <img :src="food.image">
        <div class="back" @click="showToggle()">
          <i class="icon-arrow_lift"></i>
        </div>
      </div>
      <div class="content">
        <h1 class="title">{{food.name}}</h1>
        <div class="detail">
          <span class="sell-count">月售{{food.sellCount}}份</span>
          <span class="rating">好评率{{food.rating}}</span>
        </div>
        <div class="price">
          <span class="now">¥{{food.price}}</span>
          <span class="old" v-show="food.oldPrice">¥{{food.oldPrice}}</span>
        </div>
        <div class="cartcontrol-wrapper">
          <cartcontrol :food="food"></cartcontrol>
        </div>
        <transition name="fade">
          <div @click="addCart($event)" class="buy" v-show="!food.count || food.count === 0">
            加入购物车
          </div>
        </transition>
      </div>
      <split v-show="food.info"></split>
      <div class="info" v-show="food.info">
        <h1 class="title">商品介绍</h1>
        <p class="text">{{food.info}}</p>
      </div>
      <split></split>
      <div class="rating">
        <h1 class="title">商品评价</h1>
        <div class="ratingselect">
          <div class="rating-type">
            <span class="block positive">全部</span>
            <span class="block positive">推荐</span>
            <span class="block negative">吐槽</span>
          </div>
          <div class="switch">
            <span class="icon-check_circle"></span>
            <span class="text">只看有内容的评价</span>
          </div>
          <div class="rating-wrapper">
            <ul v-show="food.ratings && food.ratings.length">
              <li v-for="rating in food.ratings" class="rating-item">
                <div class="user">
                  <span class="name">{{rating.username}}</span>
                  <img :src="rating.avatar" width="12" height="12" class="avatar">
                </div>
                <div class="time">{{rating.rateTime | time}}</div>
                <p class="text">
                  <span>{{rating.text}}</span>
                </p>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</transition>
</template>

<script type="text/ecmascript-6">
import Vue from 'vue'
import BScroll from 'better-scroll'
import cartcontrol from 'components/cartcontrol/cartcontrol'
import split from 'components/split/split'
import '../../filter/time.js'

export default {
  props: {
    food: {
      type: Object
    }
  },
  data() {
    return {
      showDetail: false
    }
  },
  methods: {
    showToggle() {
      this.showDetail = !this.showDetail
      if (this.showDetail) {
        this.$nextTick(() => {
          this._initScroll()
        })
      }
    },
    _initScroll() {
      if (!this.detailWrapper) {
        this.detailWrapper = new BScroll(this.$refs.detailWrapper, {
          click: true
        })
      } else {
        this.detailWrapper.refresh()
      }
    },
    addCart(event) {
      if (!event._constructed) {
        return
      }
      this.$set(this.food, 'count', 1)
      this.$root.eventHub.$emit('cart.add', event.target)
    }
  },
  components: {
    cartcontrol,
    split
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import '../../common/stylus/index'

.detailWrapper
  position:fixed
  left: 0
  top: 0
  bottom: 48px
  z-index: 30
  width: 100%
  background: #fff
  transition:all 0.4s ease
  &.move-enter-avtive,&.move-leave-active
    transform translate3d(0,0,0)
  &.move-enter,&.move-leave-active
    transform translate3d(100%,0,0)
  .image-header
    position: relative
    width: 100%
    height: 0
    padding-top: 100%
    img
      position: absolute
      top: 0
      left: 0
      width: 100%
      height: 100%
    .back
      position: absolute
      top: 10px
      left: 10px
      .icon-arrow_lift
        display: block
        padding: 10px
        font-size: 20px
        color: #fff
  .content
    position: relative
    padding: 18px
    .title
      line-height: 14px
      margin-bottom: 8px
      font-size: 14px
      font-weight: 700
      color: rgb(7,17,27)
    .detail
      margin-bottom: 18px
      line-height: 10px
      height: 10px
      font-size: 0
      .sell-count, .rating
        font-size: 10px
        color: rgb(147,153,159)
      .sell-count
        margin-right: 12px
    .price
      font-weight: 700
      line-height: 24px
      .now
        margin-right: 8px
        font-size: 14px
        color: rgb(240,20,20)
      .old
        text-decoration: line-through
        font-size: 10px
        color: rgb(147,153,159)
    .cartcontrol-wrapper
      position: absolute
      right: 12px
      bottom: 12px
    .buy
      position: absolute
      right: 18px
      bottom: 18px
      z-index: 10
      height: 24px
      line-height: 24px
      padding: 0 12px
      box-sizing: border-box
      border-radius: 12px
      font-size: 10px
      color: #fff
      background: rgb(0,160,220)
  .info
    padding: 18px
    .title
      line-height: 14px
      margin-bottom: 6px
      font-size: 14px
      font-weight: 500
      color: rgb(7,17,27)
    .text
      line-height: 24px
      padding: 0 8px
      font-size: 12px
      font-weight: 200
      color: rgb(77,85,93)
  .rating
    padding 18px 0
    position relative
    .title
      padding-left 18px
      font-size: 14px
      font-weight 500
      color: #07111b
    .ratingselect
      .rating-type
        padding: 18px 0
        margin: 0 18px
        border-bottom: 1px solid rgba(7,17,27,0.1)
        font-size: 0
        .block
          display: inline-block
          padding: 8px 12px
          margin-right: 8px
          border-radius: 1px
          line-height: 16px
          font-size: 12px
          color: rgb(77,85,93)
          &.active
            color: #fff
          .count
            font-size: 8px
            margin-left: 2px
          &.positive
            background: rgba(0,160,220,0.2)
            &.active
              background: rgb(0,160,220)
          &.negative
            background: rgba(77,85,93,0.2)
            &.active
              background: rgb(77,85,93)
      .switch
        padding: 12px 18px
        line-height: 24px
        border-bottom: 1px solid rgba(7,17,27,0.1)
        color: rgb(147,153,159)
        font-size: 0
        &.on
          .icon-check_circle
            color: #00c850
        .icon-check_circle
          display: inline-block
          vertical-align: top
          margin-right: 4px
          font-size: 24px
        .text
          display: inline-block
          vertical-align: top
          font-size: 12px
      .rating-wrapper
        margin: 0 18px
        .rating-item
          position: relative
          padding: 16px 0
          border-bottom: 1px solid rgba(7,17,27,0.1)
          .user
            position: absolute
            right: 0
            top: 16px
            font-size: 0
            line-height: 12px
            .name
              display: inline-block
              vertical-align: top
              margin-right: 6px
              font-size: 10px
              color: rgb(147,153,159)
            .avatar
              border-radius: 50%
          .time
            margin-bottom: 6px
            line-height: 12px
            font-size: 10px
            color: rgb(147,153,159)
          .text
            font-size: 12px
            color: rgb(7,17,27)
            line-height: 16px


</style>
