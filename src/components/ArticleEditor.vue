<template>
    <div class="ui card fluid">
        <div class="content">
            <div class="ui form">
                <div class="field">
                    <div class="ui left icon transparent input">
                        <input type="text" placeholder="title" v-model="title">
                        <i class="pencil icon"></i>
                    </div>
                    <textarea v-model="content" style="white-space: pre-line;"></textarea>
                    <button class="ui fluid right floated button" v-on:click="(event) => createArticle(event, title, content, userId)">SUBMIT ARTICLE</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  props: ['userId'],
  data () {
    return {
      title: '',
      content: '',
      newArticle: []
    }
  },
  methods: {
    /**
     * 向后端发起提交新文章
     * @param {*} event 事件
     * @param {*} title 文章的标题
     * @param {*} content 文章的内容
     * @param {*} userId 文章的发表者
     */
    createArticle: function (event, title, content, userId) {
      if (userId === '') {
        alert('select a user first.')
        return
      }
      this.$axios({
        method: 'post',
        contentType: 'application/json;charset=utf-8',
        url: 'http://localhost:8080/user/' + userId + '/article',
        data: {'title': title, 'content': content}
      }).then((response) => {
        this.$emit('startrefresharticlelist', userId)
        console.log(response.data)
      }).catch((error) => {
        console.log(error)
      })
    }
  }
}
</script>

<style scoped>
</style>
