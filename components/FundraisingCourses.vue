<template>
  <div class="flex flex-col">
    <div>正在募資的課程</div>
    <div class="grid grid-cols-4 gap-4">
      <div
        v-for="course in courses"
        :key="course.id"
      >
        <div class="image-box">
          <img
            :src="course.image"
            alt=""
            class="object-contain w-full"
          >
        </div>
        <div class="card-content">
          <div>{{ course.title }}</div>
          <div class="flex flex-row items-center">
            <div
              class="w-8 h-8 rounded-full card-image bg-center flex-shrink-0"
              :style="'background-image: url('+course.lecturers[0].avatar+');'"
            />
            <div>
              {{ course.lecturers[0].username }}
            </div>
          </div>
          <div class="relative md:flex md:justify-between md:h-28px">
            <div class="flex items-center justify-between text-gray-700 text-14px">
              <p class="w-1/2 md:hidden">
                剩 {{ countDay (course.prices[0].schedule_at) }} 天
              </p> <p class="w-1/2 text-right md:w-full md:text-left">
                已募資 103%
              </p>
            </div> <div class="flex items-center justify-center flex-1 h-28px md:h-full md:w-1/2 md:pl-10px">
              <div class="flex items-center justify-center w-full h-28px">
                <div

                  class="w-full"
                >
                  <div

                    class="flex items-center justify-between"
                  >
                    <div

                      class="w-full overflow-hidden rounded-md h-8px bg-hi-courses-box"
                    >
                      <span

                        class="block h-full rounded-md red-rate"
                        style="width: 103%;"
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
    }
  }
}
</script>
<style lang="scss">
.card-image {
  background-size: cover
}
.h-8px {
  height: 8px
}
.h-28px {
  height: 28px
}
.bg-hi-courses-box {
    --tw-bg-opacity: 1;
    background-color: rgba(245,245,245,var(--tw-bg-opacity));
}
.red-rate {
    background-image: linear-gradient(90deg,#eb6767 -.01%,#e34a4a 99.7%);
}
</style>
