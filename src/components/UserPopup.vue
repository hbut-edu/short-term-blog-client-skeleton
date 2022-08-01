<template>
    <transition name="modal">
        <div class="modal-mask">
            <div class="modal-wrapper">
                <div class="modal-container">
                    <div class="ui card">
                        <form class="ui form">
                            <div class="field">
                                <div class="ui left icon fluid input">
                                    <input ref="txtName" type="text" placeholder="Input new user name...">
                                    <i class="user icon"></i>
                                </div>
                            </div>
                            <div class="extra content">
                                <div class="ui two buttons">
                                    <button id="btnCheck" v-on:click="(event) => close(event)"
                                        class="ui blue button" type="submit">CLOSE</button>
                                    <button id="btnCheck" v-on:click="(event) => createUser(this.$refs.txtName.value, event)"
                                        class="ui green button" type="submit">SAVE</button>
                                    <div class="ui error message"></div>
                                </div>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </transition>

</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import qs from 'qs'

Vue.prototype.$axios = axios
Vue.prototype.qs = qs

export default {
  methods: {

    close: function (event) {
      this.$emit('closeuserpopup')
    },

    createUser: function (name, event) {
      if (event) {
        event.preventDefault()
      }

      this.$axios({
        method: 'post',
        contentType: 'application/json;charset=utf-8',
        url: 'http://localhost:8080/user',
        data: {'name': name}
      }).then((response) => {
        console.log(response.data)
        this.$emit('closeuserpopup')
      }).catch((error) => {
        console.log(error)
      })
    }
  }
}
</script>

<style scoped>

/* 遮罩，当窗口弹出时，让被遮住的层变暗 */
.modal-mask {
  position: fixed;
  z-index: 999;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 1s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 400px;
  margin: 0px auto;
  padding: 20px 20px;
}

.ui.card {
  padding: 10px;
}

</style>
