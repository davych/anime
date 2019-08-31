<template>
  <div class="guide_box">
    <GridProducts
      class="grid_porducts"
      ref="gridProducts"
      guide="touchProduct"
      @finish="animationFinished"
    />
  </div>
</template>

<script>
import anime from 'animejs'
import GridProducts from './grid_products'
export default {
  data: () => ({
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
      const gridProduct = this.showGridProductsAnimation()
      await gridProduct.finished
      this.$refs.gridProducts.runTouchProductAnimations()
    },
    animationFinished() {
      this.$refs.gridProducts.runTouchProductAnimations()
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
</style>
