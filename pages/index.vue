<template>
  <div>
    <Header
      :is-login="loginStatus"
      @handle-side-bar="handleSideBar"
      @login="changeLoginStatus"
    />

    <aside
      class="
        fixed
        top-0
        flex flex-col
        items-stretch
        duration-300
        bg-white
        w-375px
        h-full
        shadow-aside
        transition-position
        z-11
      "
      style="right: -381px"
    >
      <div class="relative border-gray-400 px-15px py-30px flex row-direction items-center justify-between">
        <p class="text-xl leading-none font-medium text-center text-hi-price pr-2">
          購物車
        </p>
        <button
          class="

            text-xl
            leading-none
            text-gray-700
          "
          @click="handleSideBar"
        >
          <svg
            aria-hidden="true"
            focusable="false"
            data-prefix="fas"
            data-icon="times"
            role="img"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 352 512"
            class="svg-inline--fa fa-times fa-w-11"
          >
            <path
              fill="currentColor"
              d="M242.72 256l100.07-100.07c12.28-12.28 12.28-32.19 0-44.48l-22.24-22.24c-12.28-12.28-32.19-12.28-44.48 0L176 189.28 75.93 89.21c-12.28-12.28-32.19-12.28-44.48 0L9.21 111.45c-12.28 12.28-12.28 32.19 0 44.48L109.28 256 9.21 356.07c-12.28 12.28-12.28 32.19 0 44.48l22.24 22.24c12.28 12.28 32.2 12.28 44.48 0L176 322.72l100.07 100.07c12.28 12.28 32.2 12.28 44.48 0l22.24-22.24c12.28-12.28 12.28-32.19 0-44.48L242.72 256z"
              class=""
            />
          </svg>
        </button>
      </div>
      <div
        v-if="cart.length === 0"
        class="flex flex-col items-center justify-center flex-1 w-full"
      >
        <img
          src="https://d2npjgpjzmbqfv.cloudfront.net/img/img-emptycart.d5dc721.svg"
          width="70%"
        > <p
          class="text-center text-gray-600 text-14px mt-40px"
        >
          購物車裡是空的，<br data-v-0d4e163b="">去逛逛喜歡的課程吧！
        </p> <div
          class="w-200px"
        >
          <a
            href="/groups/all"
            class="w-full default-solid-btn mt-40px mb-97px nuxt-link-active"
          >前往探索課程</a>
        </div>
      </div>
      <div
        v-else
        class="flex flex-col cursor-pointer"
      >
        <div
          v-for="(course, index) in cart"
          :key="course.id"
          class="flex flex-row items-start px-8px py-12px border-gray-400 border-b-1"
        >
          <div class="w-150px  mr-2">
            <img
              :src="course.image"
              alt=""
              class="rounded-6px"
            >
          </div>
          <div class="flex flex-col mr-1 justify-between h-84px">
            <p class="w-177px line-clamp-2">
              {{ course.title }}
            </p>
            <div class="flex flex-row text-red-1">
              <span
                class="dollar-sign font-bold mb-2px mr-4px "
              >$</span>
              <p>{{ course.prices[0].price }}</p>
            </div>
          </div>
          <div>
            <a
              class="z-3"
              @click="removeCourseByIndex(index)"
            ><svg
              aria-hidden="true"
              focusable="false"
              data-prefix="fas"
              data-icon="trash"
              role="img"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 448 512"
              class="text-gray-400 m-3px mt-5px svg-inline--fa fa-trash fa-w-14"
            ><path
              fill="currentColor"
              d="M432 32H312l-9.4-18.7A24 24 0 0 0 281.1 0H166.8a23.72 23.72 0 0 0-21.4 13.3L136 32H16A16 16 0 0 0 0 48v32a16 16 0 0 0 16 16h416a16 16 0 0 0 16-16V48a16 16 0 0 0-16-16zM53.2 467a48 48 0 0 0 47.9 45h245.8a48 48 0 0 0 47.9-45L416 128H32z"
              class=""
            /></svg></a>
          </div>
        </div>
      </div>
      <button
        class="
          side-bar-cart-button
          absolute
          bottom-0
          rounded-none
          btn
          default-solid-btn
          h-58px
          z-3
          flex
          flex-row
          justify-center
        "
      >
        <svg
          aria-hidden="true"
          focusable="false"
          data-prefix="fas"
          data-icon="shopping-cart"
          role="img"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 576 512"
          class="mr-16px svg-inline--fa fa-shopping-cart fa-w-18 fa-lg"
        >
          <path
            fill="currentColor"
            d="M528.12 301.319l47.273-208C578.806 78.301 567.391 64 551.99 64H159.208l-9.166-44.81C147.758 8.021 137.93 0 126.529 0H24C10.745 0 0 10.745 0 24v16c0 13.255 10.745 24 24 24h69.883l70.248 343.435C147.325 417.1 136 435.222 136 456c0 30.928 25.072 56 56 56s56-25.072 56-56c0-15.674-6.447-29.835-16.824-40h209.647C430.447 426.165 424 440.326 424 456c0 30.928 25.072 56 56 56s56-25.072 56-56c0-22.172-12.888-41.332-31.579-50.405l5.517-24.276c3.413-15.018-8.002-29.319-23.403-29.319H218.117l-6.545-32h293.145c11.206 0 20.92-7.754 23.403-18.681z"
            class=""
          />
        </svg>
        <p
          class="text-18px"
        >
          前往購物車
        </p>
      </button>
    </aside>

    <Fundraising-courses
      :cart="cart"
      @add-course="addCourse"
      @remove-course-by-index="removeCourseByIndex"
    />
  </div>
</template>

<script>
export default {
  data () {
    return {
      cart: [],
      isSideBarOpen: false,
      loginStatus: false
    }
  },
  methods: {
    addCourse (course) {
      this.cart.push(course)
    },
    removeCourseByIndex (index) {
      this.cart.splice(index, 1)
    },
    handleSideBar () {
      const sideBar = document.getElementsByTagName('aside')[0]
      console.log(sideBar.style.right)
      this.isSideBarOpen = !this.isSideBarOpen
      this.isSideBarOpen ? sideBar.style.right = 0 : sideBar.style.right = '-381px'
    },
    changeLoginStatus () {
      this.loginStatus = !this.loginStatus
    }
  }
}
</script>
<style lang="scss" scoped>
.shadow-aside {
  --tw-shadow: -5px 0 20px rgba(0, 0, 0, 0.05);
}
.shadow-aside,
.shadow-blur {
  box-shadow: var(--tw-ring-offset-shadow, 0 0 transparent),
    var(--tw-ring-shadow, 0 0 transparent), var(--tw-shadow);
}

.side-bar-cart-button {
  width: 100%;
}
</style>
