<template>
    <div class="ui fluid card">
        <!-- 使用v-for指令指定模板需要循环生成的部分 -->
        <div class="ui segment" v-for="article in articles" v-bind:key="article.id" v-bind:value="article.id">
            <div class="ui top right fluid attached label">{{ article.title }}</div>
            <p>{{ article.content }}</p>
        </div>
    </div>
</template>

<script>
export default {
  // props为数据入口，外部组件可以通过这个入口通过v-bind参数传入数据
  props: ['userId', 'refresh'],
  // data为视觉模型，在html代码进行绑定，绑定后只需更新视觉模型，html页面会自动更新
  data () {
    return {
      articles: [{title: 'Greentings', content: 'Please select a user first.'}]
    }
  },
  methods: {
    /**
     * 获取最新的文章列表
     */
    getAllArticles: function () {
      // TODO [请完成向后端请求特定用户发表的文章] 的代码
      // 首先需要检测UserId是否为空，获取文章数据必须要知道获取的是哪位用户的数据
      // 向后端发起获取文章数据的请求
      // 对应的Endpoint为：/user/{userId}/article
      // 响应成功后，更新最新的文章数据列表到VisualModel（this.articles）
      // 请参考UserPanel.vue的getAllUsers函数
    }
  },
  watch: {
    // 观察 refresh 变量的状态，如果发生变化，触发下面的函数
    // 由此来决定是否要更新文章列表（ArticleList），一般发生在有新文章发布后
    refresh: function (newValue, oldValue) {
      if (newValue !== oldValue && newValue === true) {
        // 请求最新的文章列表
        this.getAllArticles()

        // 告诉上级组件，更新完成了，做一些后面的处理
        this.$emit('afterrefresharticlelist')
      }
    }
  }
}
</script>

<style scoped>
.ui.segment{
    margin: 10px 10px 10px 10px;
}
</style>
