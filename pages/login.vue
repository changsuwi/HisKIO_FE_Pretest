<template>
  <div class="flex flex-col justify-center items-center">
    <div class="input-block">
      <ul>
        <li>
          <input
            v-model="email"
            type="email"
            placeholder="請輸入 HiSKIO ID"
            class="input-text"
          >
        </li>
        <li>
          <input
            v-model="password"
            type="password"
            placeholder="請輸入登入密碼"
            class="input-text"
          >
        </li>
      </ul>
    </div>
    <div class="flex flex-row items-center">
      <input type="checkbox">
      <p class="text-sm text-gray-500">
        登入註冊即代表您同意<a
          href="https://hiskio.com/user-policy"
          target="_blank"
          rel="noopener noreferrer"
          class="underline cursor-pointer"
        >使用者</a>及<a
          href="https://hiskio.com/privacy-policy"
          target="_blank"
          rel="noopener noreferrer"
          class="underline cursor-pointer"
        >隱私權政策</a>
      </p>
    </div>
    <div>
      <button
        class="mx-auto default-solid-btn w-320px mt-28px py-9px"
        @click="login"
      >
        登入
      </button>
      <button
        class="flex justify-center mx-auto text-center text-gray-600 mt-20px"
      >
        忘記密碼
      </button>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    isLogin: {
      type: Boolean,
      required: true
    }
  },
  data () {
    return {
      email: '',
      password: '',
      accessToken: ''
    }
  },
  methods: {
    async login () {
      try {
        const result = await this.$axios.$post(
          'https://api.hiskio.com/v2/auth/login',
          {
            account: this.email,
            password: this.password
          }
        )
        this.accessToken = result.accessToken
        this.$emit('login')
        this.$router.push('/')
      } catch (err) {
        alert(err)
      }
    }
  }
}
</script>
<style lang="scss" scoped>
.input-text {
  background-color: rgba(250, 250, 250, var(--tw-bg-opacity));
}
</style>
