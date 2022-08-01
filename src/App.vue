<template>
  <div id="app" class="ui grid" style="padding: 20px;">
    <div class="three wide column">
      <UserPanel @syncuserid='syncUserId' />
    </div>
    <div class="thirteen wide column">
      <ArticleEditor v-bind:userId="userId" @startrefresharticlelist='startRefreshArticleList' />
    </div>
    <div class="three wide column">
      <RecommendList v-if="false" v-bind:userId="userId" />
    </div>
    <div class="thirteen wide column">
      <ArticleList v-bind:userId="userId" v-bind:refresh="refresh" @afterrefresharticlelist='afterRefreshArticleList' />
    </div>
  </div>
</template>

<script>

import UserPanel from './components/UserPanel.vue'
import ArticleList from './components/ArticleList.vue'
import ArticleEditor from './components/ArticleEditor.vue'
import RecommendList from './components/RecommendList.vue'

export default {
  name: 'App',
  components: { UserPanel, ArticleList, ArticleEditor, RecommendList },
  data () {
    return {
      userId: '',
      refresh: false
    }
  },
  methods: {
    syncUserId: function (userId) {
      this.userId = userId
      this.refresh = true
    },
    startRefreshArticleList: function (userId) {
      this.userId = userId
      this.refresh = true
    },
    afterRefreshArticleList: function () {
      this.refresh = false
    }
  }
}

</script>

<style>
</style>
