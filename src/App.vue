<template>
  <div id="app">
    <v-header></v-header>
    <div class="tab border-1px">
      <div class="tab-item"><router-link class="" to="/goods">商品</router-link></div>
      <div class="tab-item"><router-link to="/ratings">评论</router-link></div>
      <div class="tab-item"><router-link to="/seller">商家</router-link></div>
    </div>
    <router-view></router-view>
    <div content>i am content</div>
  </div>
</template>

<script>
  import header from './components/header/header'
  export default {
    data () {
      return {
        seller: {}
      }
    },
    created () {
      this.axios.get('/api/seller').then((response) => {
        response = response.data
        if (response.errno === 0) {
          this.seller = response.data
          console.log(this.seller)
        }
      })
    },
    components: {
      'v-header': header
    }
  }
</script>
<style lang="scss" scoped>
  @import './common/scss/mixin.scss';

  .tab {
    display: flex;
    height: 40px;
    line-height: 40px;
    @include border-1px(rgba(7, 17, 27, 0.1));
    .tab-item {
      flex: 1;
      text-align: center;
      font-size: 14px;
      & > a {
        display: block;
        &.active {
          color: rgb(240, 20 , 20);
        }
      }
    }
  }
</style>
