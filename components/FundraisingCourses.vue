<template>
  <div class="flex flex-col">
    <div>正在募資的課程</div>
    <div class="grid grid-cols-3 gap-4">
      <div
        v-for="course in courses"
        :key="course.id"
      >
        <div class="image-box relative cursor-pointer">
          <img
            :src="course.image"
            alt=""
            class="object-contain w-full"
          >
          <div
            class="
              absolute
              bottom-0
              left-0
              w-full
              h-full
              transition-opacity
              duration-500
              rounded-b-none
              opacity-0
              rounded-4px
              user-teacher
              md:rounded-4px
              md:pt-0
            "
          />
          <div
            class="
              absolute
              bottom-0
              right-0
              pb-2
              pr-2
              transition-opacity
              duration-300
              collect
              z-5
              w-60px
              flex
              row-direction
              justify-end
            "
          >
            <svg
              aria-hidden="true"
              focusable="false"
              data-prefix="far"
              data-icon="bookmark"
              role="img"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 384 512"
              class="
                text-white
                transition
                duration-200
                f-a-i
                hover:text-yellow-3
                svg-inline--fa
                fa-bookmark fa-w-12 fa-lg
                mr-1
              "
            >
              <path
                fill="currentColor"
                d="M336 0H48C21.49 0 0 21.49 0 48v464l192-112 192 112V48c0-26.51-21.49-48-48-48zm0 428.43l-144-84-144 84V54a6 6 0 0 1 6-6h276c3.314 0 6 2.683 6 5.996V428.43z"
                class=""
              />
            </svg>
            <svg
              aria-hidden="true"
              focusable="false"
              data-prefix="fas"
              data-icon="shopping-cart"
              role="img"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 576 512"
              class="
                svg-inline--fa
                fa-shopping-cart fa-w-18 fa-lg
                shopping-cart
                ml-6px
                transition
                duration-200
                hover:text-yellow-3
                text-white
                mr-1
              "
              @click="handleCart(course)"
            >
              <path
                fill="currentColor"
                d="M528.12 301.319l47.273-208C578.806 78.301 567.391 64 551.99 64H159.208l-9.166-44.81C147.758 8.021 137.93 0 126.529 0H24C10.745 0 0 10.745 0 24v16c0 13.255 10.745 24 24 24h69.883l70.248 343.435C147.325 417.1 136 435.222 136 456c0 30.928 25.072 56 56 56s56-25.072 56-56c0-15.674-6.447-29.835-16.824-40h209.647C430.447 426.165 424 440.326 424 456c0 30.928 25.072 56 56 56s56-25.072 56-56c0-22.172-12.888-41.332-31.579-50.405l5.517-24.276c3.413-15.018-8.002-29.319-23.403-29.319H218.117l-6.545-32h293.145c11.206 0 20.92-7.754 23.403-18.681z"
                class=""
              />
            </svg>
          </div>
        </div>
        <div class="card-content">
          <div>
            <p class="w-full h-48px line-clamp-2 sn-640:line-clamp-1">
              {{ course.title }}
            </p>
          </div>
          <div class="flex flex-row items-center">
            <div
              class="w-8 h-8 rounded-full card-image bg-center flex-shrink-0"
              :style="
                'background-image: url(' + course.lecturers[0].avatar + ');'
              "
            />
            <div>
              <p class="pl-2 text-gray-600 line-clamp-1 md:text-14px">
                {{ course.lecturers[0].username }}
              </p>
            </div>
          </div>
          <div class="relative md:flex md:justify-between md:h-28px">
            <div
              class="flex items-center justify-between text-gray-700 text-14px"
            >
              <p class="w-1/2 hidden md:inline">
                剩 {{ countDay(course.prices[0].schedule_at) }} 天
              </p>
              <p class="w-1/2 text-right">
                已募資 103%
              </p>
            </div>
            <div
              class="
                flex
                items-center
                justify-center
                flex-1
                h-28px
              "
            >
              <div class="flex items-center justify-center w-full h-28px">
                <div class="w-full">
                  <div class="flex items-center justify-between">
                    <div
                      class="
                        w-full
                        overflow-hidden
                        rounded-md
                        h-8px
                        bg-hi-courses-box
                      "
                    >
                      <span
                        class="block h-full rounded-md red-rate"
                        style="width: 103%"
                      />
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    cart: {
      default: () => [],
      type: Array
    }
  },
  data: () => ({
    courses: []
  }),
  async fetch () {
    this.courses = await this.$axios.$get(
      'https://api.hiskio.com/v2/courses/fundraising'
    )
  },
  methods: {
    countDay (start) {
      const startDate = new Date(start)
      const now = new Date()
      const oneDay = 60 * 60 * 24 * 1000
      return 30 - Math.ceil((now - startDate) / oneDay)
    },
    handleCart (course) {
      for (let i = 0; i < this.cart.length; i++) {
        if (course.id === this.cart[i].id) {
          this.$emit('remove-course-by-index', i)
          return
        }
      }
      this.$emit('add-course', course)
    }
  }
}
</script>
<style lang="scss">
.card-image {
  background-size: cover;
}
.z-5 {
  z-index: 5;
}
.w-60px {
  width: 60px;
}
.h-8px {
  height: 8px;
}
.h-28px {
  height: 28px;
}
.h-48px {
  height: 48px;
}
.line-clamp-1 {
  -webkit-line-clamp: 1;
}

.line-clamp-2 {
  -webkit-line-clamp: 2;
}

.line-clamp-1,
.line-clamp-2 {
  overflow: hidden;
  display: -webkit-box;
  -webkit-box-orient: vertical;
}
.hover\:text-yellow-3:hover {
  --tw-text-opacity: 1;
  color: rgba(255, 168, 29, var(--tw-text-opacity));
}
.svg-inline--fa {
  width: 1rem;
}
.bg-hi-courses-box {
  --tw-bg-opacity: 1;
  background-color: rgba(245, 245, 245, var(--tw-bg-opacity));
}
.red-rate {
  background-image: linear-gradient(90deg, #eb6767 -0.01%, #e34a4a 99.7%);
}
</style>
