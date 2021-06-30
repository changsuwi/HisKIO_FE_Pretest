<template>
  <header>
    <div class="flex flex-row justify-center">
      <button class="mr-2">
        我想開課
      </button>
      <button
        v-if="isLogin"
        class="mr-2"
      >
        任務板
      </button>
      <button
        v-if="!isLogin"
        class="mr-2"
      >
        我的課程
      </button>
      <button class="w-4 mr-2">
        <svg
          data-v-6da5e576=""
          focusable="false"
          data-prefix="fas"
          data-icon="shopping-cart"
          role="img"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 576 512"
          class="svg-inline--fa fa-shopping-cart fa-w-18"
        >
          <path
            data-v-6da5e576=""
            fill="currentColor"
            d="M528.12 301.319l47.273-208C578.806 78.301 567.391 64 551.99 64H159.208l-9.166-44.81C147.758 8.021 137.93 0 126.529 0H24C10.745 0 0 10.745 0 24v16c0 13.255 10.745 24 24 24h69.883l70.248 343.435C147.325 417.1 136 435.222 136 456c0 30.928 25.072 56 56 56s56-25.072 56-56c0-15.674-6.447-29.835-16.824-40h209.647C430.447 426.165 424 440.326 424 456c0 30.928 25.072 56 56 56s56-25.072 56-56c0-22.172-12.888-41.332-31.579-50.405l5.517-24.276c3.413-15.018-8.002-29.319-23.403-29.319H218.117l-6.545-32h293.145c11.206 0 20.92-7.754 23.403-18.681z"
            class=""
          />
        </svg>
      </button>
      <button
        v-if="!isLogin"
        class="
          mr-2
          w-16
          h-8
          text-sm
          border-solid border-1
          rounded-4px
          mx-8px
          text-green-3
          border-green-3
        "
        @click="handleRoute('/login')"
      >
        登入
      </button>
      <button
        v-if="!isLogin"
        class="mr-2 w-16 h-8 text-sm text-white mx-8px rounded-4px bg-green-3"
      >
        註冊
      </button>
    </div>
  </header>
</template>
<script>
export default {
  props: {
    isLogin: {
      type: Boolean,
      required: true,
      default: false
    }
  },
  methods: {
    handleRoute (to) {
      this.$router.push(to)
    }
  }
}
</script>
<style lang="scss" scoped>
.text-green-3 {
  --tw-text-opacity: 1;
  color: rgba(48, 142, 172, var(--tw-text-opacity));
}
.border-green-3 {
  --tw-border-opacity: 1;
  border-color: rgba(48, 142, 172, var(--tw-border-opacity));
}

.border-solid {
  border-style: solid;
}

.border-1 {
  border-width: 1px;
}

.rounded-4px {
  border-radius: 4px;
}

.text-white {
  --tw-text-opacity: 1;
  color: rgba(255, 255, 255, var(--tw-text-opacity));
}

.text-sm {
  font-size: 0.875rem;
  line-height: 1.25rem;
}

.bg-green-3 {
  --tw-bg-opacity: 1;
  background-color: rgba(48, 142, 172, var(--tw-bg-opacity));
}
</style>
