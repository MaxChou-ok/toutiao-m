<template>
  <div class="my-container">

   <div v-if="user" class="header user-info">
      <div class="base-info">
        <div class="left">
          <van-image
        class="avatar"
        round
        fit="cover"
       :src="userInfo.photo"/>
       <span class="name">{{ userInfo.name }}</span>
        </div>
        <div class="right">
          <van-button size="mini" round>编辑资料</van-button>
        </div>
      </div>
     <div class="data-stats">
    <div class="data-item">
      <span class="count">{{userInfo.art_count}}</span>
      <span class="text">头条</span>
    </div>
    <div class="data-item">
       <span class="count">{{userInfo.follow_count}}</span>
      <span class="text">关注</span>
    </div>
    <div class="data-item">
       <span class="count">{{userInfo.fans_count}}</span>
      <span class="text">粉丝</span>
    </div>
    <div class="data-item">
       <span class="count">{{userInfo.like_count}}</span>
      <span class="text">获赞</span>
    </div>
     </div>
    </div>

    <div v-else class="header not-login">
      <div class="login-btn" @click="$router.push('./login')">
        <img class="mobile-img" src="~@/assets/mobile.png" alt="">
        <span class="text">登录 / 注册</span>
      </div>
    </div>

    <!-- 导航 -->
    <van-grid class="grid-nav" :column-num="2" clickable>
  <van-grid-item class="grid-item">
    <i slot="icon" class="toutiao toutiao-shoucang"></i>
    <span slot="text" class="text">收藏</span>
  </van-grid-item>
  <van-grid-item class="grid-item">
    <i slot="icon" class="toutiao toutiao-lishi"></i>
    <span slot="text" class="text">历史</span>
  </van-grid-item>
</van-grid>

  <van-cell class="xxtz" title="消息通知" is-link />
  <van-cell class="mb-9" title="秦浩凯同学" is-link />
   <van-cell
   v-if="user"
   title="退出登录"
   class="logout-cell"
   clickable
   @click="onLogout"/>

  </div>
</template>

<script>
import { mapState } from 'vuex'
import { getUserInfo } from '@/api/user'

export default {
  name: 'MyIndex',
  components: {},
  props: {},
  data () {
    return {
      userInfo: {

      }
    }
  },
  computed: {
    ...mapState(['user'])
  },
  watch: {},
  created () {
    if (this.user) {
      this.loadUserInfo()
    }
  },
  mounted () {},
  methods: {
    onLogout () {
    // 退出登录提示
      this.$dialog.confirm({
        title: '确认退出吗？'
      })
        .then(() => {
          this.$store.commit('setUser', null)
        })
        .catch(() => {
        // on cancel
        })
    },
    async loadUserInfo () {
      try {
        const { data } = await getUserInfo()
        this.userInfo = data.data
      } catch (err) {
        this.$toast('获取数据失败，请稍后重试')
      }
    }
  }
}
</script>

<style scoped lang="less">
.my-container {
  .header {
    height: 361px;
    background:url("~@/assets/banner.png")
  }
  .not-login {
  display: flex;
  justify-content: center;
  align-items: center;
  .login-btn {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    .mobile-img {
      width: 132px;
      height: 132px;
      margin-bottom: 15px;
      }
     .text {
       font-size: 28px;
       color: #fff;
     }
  }
  }
  .user-info {
    .base-info {
    padding: 76px 32px 23px;
    box-sizing: border-box;
    height: 231px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    .left {
      display: flex;
      align-items: center;
      .avatar {
        width: 132px;
        height: 132px;
          margin-right: 23px;
          border: 4px solid #fff;
      }
      .name {
        font-size: 30px;
        color: #fff;
      }
    }
    }
    .data-stats{
    // height: 130px;
    display: flex;
    .data-item {
      height: 130px;
      flex: 1;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      .count {
        font-size: 36px;
        color: #fff;
      }
      .text {
        font-size: 36px;
        color: #fff;
      }
    }
    }
  }
  .grid-nav {
    .grid-item{
      height: 141px;
      i.toutiao {
        font-size: 45px;
      }
      .toutiao-shoucang {
        color: #eb5253;
      }
      .toutiao-lishi {
        color: #ff9d1d;
      }
      span.text {
        font-size: 28px;
      }
    }
  }
  .logout-cell {
    color:#d86262;
    text-align: center;
  }
  .mb-9 {
    margin-bottom: 7px;
    margin-top: 1.5px;
  }
  .xxtz {
    margin-top: 6px;
  }
}
</style>
