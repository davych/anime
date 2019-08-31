<template>
  <div class="touch_point" ref="touchPoint">
    <div class="touch_point_in"></div>
  </div>
</template>

<script>
import anime from 'animejs'
export default {
  data: () => ({
    rate:1 
  }),
  components: {},
  mounted() {},
  methods: {
    move(styles) {
      return anime({
        targets: this.$refs.touchPoint,
        opacity: [0, 1],
        ...styles,
        scale: [0, 1],
        duration: 800 * this.rate,
        easing: 'easeOutExpo'
      })
    },
    scaleMove(x, y) {
      return anime({
        targets: this.$refs.touchPoint,
        translateX: x,
        translateY: y,
        duration: 1500,
        easing: 'easeOutExpo'
      })
    },
    scale() {
      return anime({
        targets: this.$refs.touchPoint,
        scale: [1.3, 1],
        duration: 600,
        easing: 'easeOutExpo'
      })
    },
    hide() {
      return anime({
        targets: this.$refs.touchPoint,
        opacity: [1, 0],
        scale: [1, 0],
        duration: 1200 * this.rate,
        easing: 'easeOutBounce'
      })
    },
    show() {
      return anime({
        targets: this.$refs.touchPoint,
        opacity: [0, 1],
        scale: [0, 1],
        duration: 1200 * this.rate,
        easing: 'easeOutBounce'
      })
    }
  }
}
</script>
<style scoped>
.touch_point {
  opacity: 0;
  width: .2rem;
  height: .2rem;
  padding: 5px;
  background: rgba(255, 255, 255, 0.5);
  border-radius: 1000px;
}
.touch_point_in {
  width: .2rem;
  height: .2rem;
  background: white;
  border-radius: 100px;
}
</style>
