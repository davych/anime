<template>
  <div class="welcome_page">
    <div class="swiper-container">
      <div class="swiper-wrapper">
        <div class="swiper-slide page">
          <GuideTouchMove v-if="active === 0" />
        </div>
        <div class="swiper-slide page">
          <GuideTouchScale v-if="active === 1" />
        </div>
        <div class="swiper-slide page">
          <GuideTouchProduct v-if="active === 2" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import anime from 'animejs'
import Swiper from 'swiper'
import GuideTouchMove from './sprites/guide_touch_move'
import GuideTouchScale from './sprites/guide_touch_scale'
import GuideTouchProduct from './sprites/guide_touch_product'
export default {
  components: {
    GuideTouchMove,
    GuideTouchScale,
    GuideTouchProduct
  },
  data: () => ({
    active: 0
  }),
  mounted() {
    const getThis = this
    var mySwiper = new Swiper('.swiper-container', {
      on: {
        slideChangeTransitionEnd: function() {
          getThis.active = this.activeIndex
        }
      },
      autoplay: false //可选选项，自动滑动
    })
  }
}
</script>

<style scoped>
.welcome_page {
  width: 100%;
  height: 100%;
  right: 0;
  left: 0;
  position: fixed;
  top: 0;
  bottom: 0;
}
.page {
  background: #f21034;
}
.swiper-container {
  width: 100%;
  height: 100%;
  margin-left: auto;
  margin-right: auto;
}
</style>
