<template>
  <div class="guide_box">
    <div class="guide_logo_box">
      <img src="../../assets/logo.png" class="logo" alt />
    </div>
    <GridProducts
      class="grid_porducts"
      ref="gridProducts"
      @finish="runAnimation"
      v-if="showGridProducts"
    />
  </div>
</template>

<script>
import anime from 'animejs'
import GridProducts from './grid_products'
import { setTimeout } from 'timers'
export default {
  data: () => ({
    showGridProducts: false,
    rate: 0.5
  }),
  components: {
    GridProducts
  },
  async mounted() {
    await this.runAnimation()
  },
  methods: {
    async runAnimation() {
      const logoAnimation = this.showLogoAnimation()
      await logoAnimation.finished
      this.showGridProducts = true
      setTimeout(async () => {
        const gridProductsAnimation = this.showGridProductsAnimation()
        await gridProductsAnimation.finished
        this.$refs.gridProducts.runTouchMoveAnimations()
      }, 1)
    },
    showLogoAnimation() {
      this.showGridProducts = false
      return anime({
        targets: '.guide_logo_box',
        opacity: [0, 1, 1, 1, 1, 0],
        duration: 2250 * this.rate,
        easing: 'easeInOutQuad'
      })
    },
    showGridProductsAnimation() {
      return anime({
        targets: this.$refs.gridProducts.$el,
        opacity: [0, 1],
        duration: 2200 * this.rate,
        easing: 'easeInOutQuad'
      })
    }
  }
}
</script>
<style scoped>
@import url(./sprite.css);
.grid_porducts {
  opacity: 0;
}
.guide_logo_box {
  position: absolute;
  top: 50%;
  width: 100%;
  opacity: 0;
  transform: translate(0, -50%);
}
.guide_logo_box img {
  text-align: center;
  width: 80%;
}
</style>
