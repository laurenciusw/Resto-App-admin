<script>
import Login from './components/login.vue'
import Register from './components/register.vue'
import Sidebar from './components/sidebar.vue'
import Home from './components/home.vue'

import axios from 'axios'

const baseUrl = 'http://localhost:3000'

export default {
  data() {
    return {
      currentPage: null,
      cuisine: [],
      categories: [],
      histories: [],
      cuisineDetail: ''
    }
  },
  components: {
    // Navbar,
    Login,
    Register,
    Sidebar,
    Home
  },
  created() {
    if (localStorage.access_token) {
      this.currentPage = 'home'
    } else {
      this.currentPage = 'login'
    }
  },
  methods: {
    handleLogout() {
      localStorage.clear()
      this.currentPage = 'login'
    },

    toRegister() {
      this.currentPage = 'register'
    },

    toLogin() {
      this.currentPage = 'login'
    },

    async handleLogin(dataInput) {
      try {
        const { data } = await axios({
          method: 'post',
          url: `${baseUrl}/auth/login`,
          data: dataInput
        })

        localStorage.access_token = data.acces_token
        this.currentPage = 'home'
      } catch (error) {
        Swal.fire({
          icon: 'error',
          title: error.response.data.message
        })
      }
    },

    async handleRegister(userData) {
      try {
        const { data } = await axios({
          method: 'post',
          url: `${baseUrl}/users/register`,
          data: userData
        })

        console.log(data)
        this.currentPage = 'login'
      } catch (error) {
        Swal.fire({
          icon: 'error',
          title: error.response.data.message
        })
      }
    },

    async handleFetchCuisine() {
      try {
        const { data } = await axios({
          method: 'get',
          url: `${baseUrl}/cuisines`,
          headers: {
            acces_token: localStorage.access_token
          }
        })

        this.cuisine = data
      } catch (error) {
        console.log(error.response.data.message)
      }
    },

    async handleFetchCategory() {
      try {
        const { data } = await axios({
          method: 'get',
          url: `${baseUrl}/categories`,
          headers: {
            acces_token: localStorage.access_token
          }
        })

        this.categories = data
      } catch (error) {
        console.log(error.response.data.message)
      }
    },

    async handleFetchHistory() {
      try {
        const { data } = await axios({
          method: 'get',
          url: `${baseUrl}/histories`
        })

        this.histories = data
      } catch (error) {
        console.log(error.response.data.message)
      }
    },

    async handleAddCuisine(newCuisine) {
      try {
        const { data } = await axios({
          method: 'post',
          url: `${baseUrl}/cuisines`,
          data: newCuisine,
          headers: {
            acces_token: localStorage.access_token
          }
        })
        await this.handleFetchCuisine()
        this.$refs.home.changeSection('newCuisine')
      } catch (error) {
        Swal.fire({
          icon: 'error',
          title: error.response.data.message
        })
      }
    },

    async detailCuisine(id) {
      try {
        const { data } = await axios({
          method: 'get',
          url: `${baseUrl}/cuisines/${id}`,
          headers: {
            acces_token: localStorage.access_token
          }
        })
        this.$refs.home.changeSection('cuisineForm')
        console.log(data)
        this.cuisineDetail = data
      } catch (error) {
        console.log(error.response.data.message)
      }
    },

    async editCuisine(newCuisine, id) {
      console.log(newCuisine)
      try {
        await axios({
          method: 'put',
          url: `${baseUrl}/cuisines/${id}`,
          headers: {
            acces_token: localStorage.access_token
          },
          data: newCuisine
        })
        await this.handleFetchCuisine()
        this.$refs.home.changeSection('newCuisine')
      } catch (error) {
        Swal.fire({
          icon: 'error',
          title: error.response.data.message
        })
      }
    },

    async googlelogin(res) {
      try {
        const google_token = res.credential
        const { data } = await axios({
          method: 'post',
          url: `${baseUrl}/auth/login-google`,
          headers: { google_token }
        })

        localStorage.access_token = data.acces_token
        this.currentPage = 'home'
      } catch (error) {}
    },

    async editStatus(id, newStatus) {
      console.log(id, newStatus, 'dari app')
      try {
        await axios({
          method: 'patch',
          url: `${baseUrl}/cuisines/${id}`,
          headers: {
            acces_token: localStorage.access_token
          },
          data: { status: newStatus }
        })
        await this.handleFetchCuisine()
        this.$refs.home.changeSection('newCuisine')
      } catch (error) {
        console.log(error.response.data.message)
      }
    }
  }
}
</script>

<template>
  <div>
    <Login
      v-if="currentPage === 'login'"
      @handleLogin="handleLogin"
      @toRegister="toRegister"
      @googlelogin="googlelogin"
    />
    <Register
      v-if="currentPage == 'register'"
      @handleRegister="handleRegister"
      @toLogin="toLogin"
      @googlelogin="googlelogin"
    />
    <Home
      v-if="currentPage == 'home'"
      @handleLogout="handleLogout"
      @handleFetchCuisine="handleFetchCuisine"
      :cuisine="cuisine"
      @handleFetchCategory="handleFetchCategory"
      :categories="categories"
      @handleFetchHistory="handleFetchHistory"
      :histories="histories"
      @handleAddCuisine="handleAddCuisine"
      ref="home"
      @detailCuisine="detailCuisine"
      :cuisineDetail="cuisineDetail"
      @editCuisine="editCuisine"
      @editStatus="editStatus"
    />
  </div>
</template>

<style></style>
