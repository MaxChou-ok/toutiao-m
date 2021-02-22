<template>
  <div class="article-list">
      <van-list
      v-model="loading"
      :finished="finished"
      finished-text="没有更多了"
      :error.sync="error"
  error-text="请求失败，点击重新加载"
      @load="onLoad">
<van-cell
 v-for="(article, index) in list"
  :key="index"
   :title="article.title"
   ></van-cell>
      </van-list>
  </div>
</template>

<script>

import { getArticles } from '@/api/article'
export default {
  name: 'ArticleList',
  components: {},
  props: {
    channel: {
      type: Object,
      required: true
    }
  },
  data () {
    return {
      list: [],
      loading: false,
      finished: false,
      timestamp: null,
      error: false
    }
  },
  computed: {},
  watch: {},
  created () {},
  mounted () {},
  methods: {
    async onLoad () {
      try {
        const { data } = await getArticles({
          channel_id: this.channel.id,
          timestamp: this.timestamp || Date.now(),
          with_top: 1
        })
        if (Math.random() > 0.5) {
          JSON.parse('dsnajndjsa')
        }

        const { results } = data.data
        this.list.push(...results)
        this.loading = false
        if (results.length) {
          this.timestamp = data.data.pre_timestamp
        } else {
          this.finished = true
        }
      } catch (err) {
        console.log('请求数据失败', err)
      }
    }
  }
}
</script>

<style scoped lang="less">

</style>
