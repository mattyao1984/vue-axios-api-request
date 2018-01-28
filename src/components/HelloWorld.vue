<script>
import Vue from 'vue'
import Axios from 'axios'
import VueAxios from 'vue-axios'

Vue.use(VueAxios, Axios)

export default {
  data () {
    return {
      username: '',
      data: [],
      errorMsg: ''
    }
  },

  methods: {
    search () {
      const api = `https://api.github.com/users/${this.username}`

      Vue.axios.get(api).then(response => {
        this.data = response.data
      }).catch(error => {
        this.errorMsg = `No user has been found! Error: ${error}`
        this.data = []
      })
    }
  }
}
</script>

<template>
  <div id="app">
    <form @submit.prevent="search">
      <input v-model="username" placeholder="Enter a Github username" />
    </form>

    <p v-if="data.login">
      {{ data.login }} is updated at {{ data.updated_at }}
    </p>
    <p v-else>
      {{ data.errorMsg }}
    </p>
  </div>
</template>
