<script>
import googlelogin from './googlelogin.vue'
export default {
  data() {
    return {
      dataInput: {
        email: null,
        password: null
      }
    }
  },
  methods: {
    doLogin() {
      this.$emit('handleLogin', this.dataInput)
    },
    toRegister() {
      this.$emit('toRegister')
    },
    googlelogin(data) {
      console.log(data)
      this.$emit('googlelogin', data)
    }
  },
  components: {
    googlelogin
  }
}
</script>

<template>
  <div class="max-w-lg mx-auto my-10 bg-white p-8 rounded-xl shadow shadow-slate-300">
    <h1 class="text-4xl font-medium">Login</h1>
    <p class="text-slate-500">Hi, Welcome back 👋</p>

    <googlelogin @googlelogin="googlelogin" />

    <form @submit.prevent="doLogin" class="my-10">
      <div class="flex flex-col space-y-5">
        <label for="email">
          <p class="font-medium text-slate-700 pb-2">Email address</p>
          <input
            v-model="dataInput.email"
            id="email"
            name="email"
            type="email"
            class="w-full py-3 border border-slate-200 rounded-lg px-3 focus:outline-none focus:border-slate-500 hover:shadow"
            placeholder="Enter email address"
          />
        </label>
        <label for="password">
          <p class="font-medium text-slate-700 pb-2">Password</p>
          <input
            v-model="dataInput.password"
            id="password"
            name="password"
            type="password"
            class="w-full py-3 border border-slate-200 rounded-lg px-3 focus:outline-none focus:border-slate-500 hover:shadow"
            placeholder="Enter your password"
          />
        </label>
        <div class="flex flex-row justify-between"></div>
        <button
          class="w-full py-3 font-medium text-white bg-indigo-600 hover:bg-indigo-500 rounded-lg border-indigo-500 hover:shadow inline-flex space-x-2 items-center justify-center"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            stroke-width="2"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M11 16l-4-4m0 0l4-4m-4 4h14m-5 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h7a3 3 0 013 3v1"
            />
          </svg>
          <span>Login</span>
        </button>
        <p class="text-center">
          Not registered yet?
          <a
            @click.prevent="toRegister"
            href="#"
            class="text-indigo-600 font-medium inline-flex space-x-1 items-center"
            ><span>Register now </span
            ><span
              ><svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-4 w-4"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
                stroke-width="2"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"
                /></svg></span
          ></a>
        </p>
      </div>
    </form>
  </div>
</template>

<style>
:root {
  font-family: 'Inter', sans-serif;
}
@supports (font-variation-settings: normal) {
  :root {
    font-family: 'Inter var', sans-serif;
  }
}
</style>
