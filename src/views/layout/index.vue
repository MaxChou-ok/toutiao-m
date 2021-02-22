<template>
<div class="layout-container">
  <router-view />

    <!-- 底部导航栏 -->
<van-tabbar route class="layout-tabber">
  <van-tabbar-item to="/">
      <i slot="icon" class="toutiao toutiao-shouye"></i>
     <span class="text">首页</span>
    </van-tabbar-item>
  <van-tabbar-item to="/qa">
      <i slot="icon" class="toutiao toutiao-wenda"></i>
      <span class="text">问答</span>
      </van-tabbar-item>
  <van-tabbar-item to="/video">
      <i slot="icon" class="toutiao toutiao-shipin"></i>
      <span class="text">视频页</span>
      </van-tabbar-item>
  <van-tabbar-item to="/my">
      <i slot="icon" class="toutiao toutiao-wode"></i>
      <span class="text">{{ $store.state.user ? '我的' : '未登录'}}</span>
      </van-tabbar-item>
</van-tabbar>
</div>
</template>

<script>
export default {
  name: 'LayoutIndex',
  components: {},
  props: {},
  data () {
    return {

    }
  },
  computed: {},
  watch: {},
  created () {},
  mounted () {},
  methods: {}
}
</script>

<style scoped lang="less">
.layout-container {
  .layout-tabber {
       i.toutiao {
           font-size: 40px
           }
      span.text {
        font-size : 20px; ;
      }
        }
      }
</style>
