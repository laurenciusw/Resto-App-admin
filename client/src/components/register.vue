<template>
  <div class="min-h-screen flex flex-col items-center justify-center bg-gray-100">
    <div
      class="flex flex-col bg-white shadow-md px-4 sm:px-6 md:px-8 lg:px-10 py-8 rounded-3xl w-50 max-w-md"
    >
      <div class="font-medium self-center text-xl sm:text-3xl text-gray-800">Join us Now</div>
      <div class="mt-4 self-center text-xl sm:text-sm text-gray-800">
        Enter your credentials to get access account
      </div>

      <!-- username -->

      <div class="mt-10">
        <form @submit.prevent="doRegister">
          <div class="flex flex-col mb-5">
            <label for="username" class="mb-1 text-xs tracking-wide text-gray-600">Username:</label>
            <div class="relative">
              <div
                class="inline-flex items-center justify-center absolute left-0 top-0 h-full w-10 text-gray-400"
              >
                <i class="fas fa-user text-blue-500"></i>
              </div>

              <input
                v-model="userData.username"
                id="username"
                type="username"
                name="username"
                class="text-sm placeholder-gray-500 pl-10 pr-4 rounded-2xl border border-gray-400 w-full py-2 focus:outline-none focus:border-blue-400"
                placeholder="Enter your name"
              />
              <div v-if="errMsg">{{ errMsg }}</div>
            </div>
          </div>

          <!-- email -->

          <div class="flex flex-col mb-5">
            <label for="email" class="mb-1 text-xs tracking-wide text-gray-600"
              >E-Mail Address:</label
            >
            <div class="relative">
              <div
                class="inline-flex items-center justify-center absolute left-0 top-0 h-full w-10 text-gray-400"
              >
                <i class="fas fa-at text-blue-500"></i>
              </div>

              <input
                v-model="userData.email"
                id="email"
                type="email"
                name="email"
                class="text-sm placeholder-gray-500 pl-10 pr-4 rounded-2xl border border-gray-400 w-full py-2 focus:outline-none focus:border-blue-400"
                placeholder="Enter your email"
              />
            </div>
          </div>

          <!-- password -->

          <div class="flex flex-col mb-6">
            <label for="password" class="mb-1 text-xs sm:text-sm tracking-wide text-gray-600"
              >Password:</label
            >
            <div class="relative">
              <div
                class="inline-flex items-center justify-center absolute left-0 top-0 h-full w-10 text-gray-400"
              >
                <span>
                  <i class="fas fa-lock text-blue-500"></i>
                </span>
              </div>

              <input
                v-model="userData.password"
                id="password"
                type="password"
                name="password"
                class="text-sm placeholder-gray-500 pl-10 pr-4 rounded-2xl border border-gray-400 w-full py-2 focus:outline-none focus:border-blue-400"
                placeholder="Enter your password"
              />
            </div>
          </div>

          <!-- phonenumber -->

          <div class="flex flex-col mb-5">
            <label for="phonenumber" class="mb-1 text-xs tracking-wide text-gray-600"
              >Phone number:</label
            >
            <div class="relative">
              <div
                class="inline-flex items-center justify-center absolute left-0 top-0 h-full w-10 text-gray-400"
              >
                <i class="fas fa-user text-blue-500"></i>
              </div>

              <input
                v-model="userData.phonenumber"
                id="phonenumber"
                type="phonenumber"
                name="phonenumber"
                class="text-sm placeholder-gray-500 pl-10 pr-4 rounded-2xl border border-gray-400 w-full py-2 focus:outline-none focus:border-blue-400"
                placeholder="Enter your phonenumber"
              />
            </div>
          </div>

          <!-- address -->

          <div class="flex flex-col mb-5">
            <label for="address" class="mb-1 text-xs tracking-wide text-gray-600">Address:</label>
            <div class="relative">
              <div
                class="inline-flex items-center justify-center absolute left-0 top-0 h-full w-10 text-gray-400"
              >
                <i class="fas fa-user text-blue-500"></i>
              </div>

              <input
                v-model="userData.address"
                id="address"
                type="address"
                name="address"
                class="text-sm placeholder-gray-500 pl-10 pr-4 rounded-2xl border border-gray-400 w-full py-2 focus:outline-none focus:border-blue-400"
                placeholder="Enter your address"
              />
            </div>
          </div>

          <div class="flex w-full">
            <button
              type="submit"
              class="flex mt-2 items-center justify-center focus:outline-none text-white text-sm sm:text-base bg-blue-500 hover:bg-blue-600 rounded-2xl py-2 w-full transition duration-150 ease-in"
            >
              <span class="mr-2 uppercase">Sign Up</span>
              <span>
                <svg
                  class="h-6 w-6"
                  fill="none"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  viewBox="0 0 24 24"
                  stroke="currentColor"
                >
                  <path d="M13 9l3 3m0 0l-3 3m3-3H8m13 0a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
              </span>
            </button>
          </div>
        </form>
      </div>
    </div>
    <div class="flex justify-center items-center mt-6">
      <a
        href="#"
        target="_blank"
        class="inline-flex items-center text-gray-700 font-medium text-xs text-center"
      >
        <span class="ml-2"
          >You have an account?
          <a @click.prevent="toLogin" href="#" class="text-xs ml-2 text-blue-500 font-semibold"
            >Login here</a
          ></span
        >
        <googlelogin @googlelogin="googlelogin" />
      </a>
    </div>
  </div>
</template>

<script>
import googlelogin from './googlelogin.vue'
export default {
  data() {
    return {
      userData: {
        username: null,
        email: null,
        password: null,
        phonenumber: null,
        address: null
      },
      errMsg: ''
    }
  },
  methods: {
    doRegister() {
      this.$emit('handleRegister', this.userData)
    },

    toLogin() {
      this.$emit('toLogin')
    },
    googlelogin(data) {
      this.$emit('googlelogin', data)
    }
  },
  components: {
    googlelogin
  },
  watch: {
    'userData.username': function (newValue) {
      if (newValue.length < 1) {
        this.errMsg = 'username must be morethan 1 character'
      } else {
        this.errMsg = ''
      }
    }
  }
}
</script>

<style></style>
