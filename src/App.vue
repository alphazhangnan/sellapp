<template>
<div id="app">
  <v-header :seller="seller"></v-header>
  <div class="tab">
    <div class="tab-item">
      <router-link to="/goods">商品</router-link>
    </div>
    <div class="tab-item">
      <router-link to="/ratings">评论</router-link>
    </div>
    <div class="tab-item">
      <router-link to="/seller">商家</router-link>
    </div>
  </div>
  <router-view :seller="seller"></router-view>
</div>
</template>

<script>
import header from 'components/header/header'
import axios from 'axios'
const ERR_OK = 0

export default {
  data() {
    return {
      seller: {}
    }
  },
  created() {
    axios.get('static/data.json').then((response) => {
      this.seller = response.data.seller
    })
  },

  components: {
    'v-header': header
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">

@import 'common/stylus/index'

  .tab
    display: flex;
    width: 100%;
    height: 40px;
    line-height: 40px;
    boder-1px(rgba(7,17,27,0.1))
    .tab-item
      flex:1;
      text-align: center;
      & > a
        display: block
        text-decoration : none
        font-size: 14px
        color: rgb(77,85,93)
        &.active
          color: rgb(240,20,20)

</style>
