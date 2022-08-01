<template>
    <div class="ui fluid card">
        <div class="content">
            <div class="description">
                <select class="ui fluid dropdown" v-model="userId">
                    <option v-for="user in users" v-bind:key="user.id" v-bind:value="user.id">
                        {{ user.name }}
                    </option>
                </select>
            </div>
        </div>
        <div class="ui bottom attached button" v-on:click="(event) => showUserPopup(event)">
            <i class="add icon"></i>
            CREATE USER
        </div>
        <UserPopup v-if="showModal" @closeuserpopup="(event) => closeUserPopUp(event)">
        </UserPopup>
    </div>
</template>

<script>

import UserPopup from './UserPopup.vue'

export default {
  components: { UserPopup },
  data () {
    return {
      userId: '',
      users: [],
      showModal: false
    }
  },
  mounted: function () {
    this.getAllUsers()
  },
  methods: {

    getAllUsers: function () {
      this.$axios({
        method: 'get',
        url: 'http://localhost:8080/user/'
      }).then((response) => {
        this.users = response.data
      }).catch((error) => {
        console.log(error)
      })
    },

    showUserPopup: function (event) {
      this.showModal = true
    },

    closeUserPopUp: function (event, isCreated) {
      this.showModal = false
      this.getAllUsers()
    }
  },
  watch: {
    userId: function (newValue, oldValue) {
      this.$emit('syncuserid', newValue)
    }
  }
}
</script>

<style scoped>
</style>
