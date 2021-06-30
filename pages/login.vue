<template>
  <div class="flex flex-col justify-center items-center">
    <div class="input-block">
      <ul>
        <li>
          <input
            type="email"
            placeholder="請輸入 HiSKIO ID"
            class="input-text"
            v-model="email"
          />
        </li>
        <li>
          <input
            type="password"
            placeholder="請輸入登入密碼"
            class="input-text"
            v-model="password"
          />
        </li>
      </ul>
    </div>
    <div class="flex flex-row items-center">
      <input type="checkbox" />
      <p class="text-sm text-gray-500">
        登入註冊即代表您同意<a
          href="https://hiskio.com/user-policy"
          target="_blank"
          rel="noopener noreferrer"
          class="underline cursor-pointer"
          >使用者</a
        >及<a
          href="https://hiskio.com/privacy-policy"
          target="_blank"
          rel="noopener noreferrer"
          class="underline cursor-pointer"
          >隱私權政策</a
        >
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
  data() {
    return {
      email: "",
      password: "",
      accessToken: "",
    };
  },
  methods: {
    async login() {
      try {
        let result = await this.$axios.$post(
          "https://api.hiskio.com/v2/auth/login",
          {
            account: this.email,
            password: this.password,
          }
        );
        this.accessToken = result.accessToken;
        this.$router.push("/");
      } catch (err) {
        alert(err);
      }
    },
  },
};
</script>
<style lang="scss" scoped>
.input-text {
  background-color: rgba(250, 250, 250, var(--tw-bg-opacity));
}
.py-9px {
  padding-top: 9px;
  padding-bottom: 9px;
}
.w-320px {
  width: 320px;
}
.mt-28px {
  margin-top: 28px;
}

.default-btn,
.default-solid-btn {
  display: flex;
  height: 40px;
  width: 200px;
  align-items: center;
  justify-content: center;
  --tw-bg-opacity: 1;
  --tw-text-opacity: 1;
}

.default-solid-btn {
  border-radius: 4px;
  background-color: rgba(23, 143, 172, var(--tw-bg-opacity));
  color: rgba(255, 255, 255, var(--tw-text-opacity));
}

.text-gray-600 {
  --tw-text-opacity: 1;
  color: rgba(140, 140, 140, var(--tw-text-opacity));
}
</style>