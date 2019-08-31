<template>
  <div class="grid_product_box">
    <table class="products_gallery" ref="gallery">
      <tbody>
        <tr :style="{height: rowHeight}">
          <td>
            <img src="../../assets/product.png" />
          </td>
          <td>
            <img src="../../assets/product.png" />
          </td>
          <td>
            <img src="../../assets/product.png" />
          </td>
        </tr>
        <tr :style="{height: rowHeight}">
          <td>
            <img src="../../assets/product.png" />
          </td>
          <td>
            <TouchPoint
              ref="touchScaleBottom"
              class="touch_scale_bottom"
              v-if="guide === 'touchScale'"
            />
            <img src="../../assets/product.png" ref="centerProduct" />
            <TouchPoint ref="touchMovePoint" class="touch_move" v-if="guide === 'touchMove'" />
            <TouchPoint
              ref="touchProductPoint"
              class="touch_product"
              v-if="guide === 'touchProduct'"
            />
            <TouchPoint ref="touchScaleTop" class="touch_scale_top" v-if="guide === 'touchScale'" />
          </td>
          <td>
            <img src="../../assets/product.png" />
          </td>
        </tr>
        <tr :style="{height: rowHeight}">
          <td>
            <img src="../../assets/product.png" />
          </td>
          <td>
            <img src="../../assets/product.png" ref="gridItem" />
            <div class="product_infos" ref="productInfos">
              <div class="info_title" ref="productTitle">这是title</div>
              <div class="info_shopcard" ref="productShopcard">这是shopcard</div>
            </div>
          </td>
          <td>
            <img src="../../assets/product.png" />
          </td>
        </tr>

        <tr :style="{height: rowHeight}">
          <td>
            <img src="../../assets/product.png" />
          </td>
          <td>
            <img src="../../assets/product.png" />
          </td>
          <td>
            <img src="../../assets/product.png" />
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import anime from 'animejs'
import TouchPoint from './touch_point'
import { MOVE_DATAS, GRID_PRODUCTS_IMAGE } from './consts'
export default {
  components: {
    TouchPoint
  },
  props: {
    guide: {
      default: 'touchMove',
      stype: String
    }
  },
  data: () => ({
    productImg: GRID_PRODUCTS_IMAGE,
    rowHeight: '',
    rate: 0.4
  }),
  methods: {
    async runTouchMoveAnimations() {
      const touchMove = this.$refs.touchMovePoint.move({
        right: '20%',
        bottom: '30%'
      })
      await touchMove.finished
      const galleryMove = anime({
        targets: this.$refs.gallery,
        translateX: MOVE_DATAS,
        translateY: [0, 80, 0],
        duration: 1500 * this.rate,
        easing: 'cubicBezier(.5, .05, .1, .3)'
      })
      await galleryMove.finished
      const toucherHide = this.$refs.touchMovePoint.hide()
      await toucherHide.finished
      this.$emit('finish')
    },
    async runTouchScaleAnimations() {
      const touchPointBottomShow = this.$refs.touchScaleBottom.show()
      const touchPointTopShow = this.$refs.touchScaleTop.show()
      await touchPointTopShow.finished
      const touchPointBottomMove = this.$refs.touchScaleBottom.scaleMove(
        [0, 30, 0],
        [0, -40, 0]
      )
      const touchPointTopMove = this.$refs.touchScaleTop.scaleMove(
        [0, -30, 0],
        [0, 40, 0]
      )
      const galleryScale = anime({
        targets: this.$refs.gallery,
        scale: [1, 0.6, 1],
        duration: 1500,
        easing: 'easeOutExpo'
      })
      //grid_item
      this.hideGridItem()
      const showProductsInfos = this.showProductsInfos()
      await showProductsInfos.finished
      this.showGridItem()
      this.hideProductionInfos()
      this.$emit('finish')
    },
    async runTouchProductAnimations() {
      const touchMove = this.$refs.touchProductPoint.move({
        right: '45%',
        bottom: '30%'
      })
      await touchMove.finished
      const touchScale = this.$refs.touchProductPoint.scale()

      const centerProduct = anime({
        targets: this.$refs.centerProduct,
        scale: [1.2, 1],
        opacity: [0.4, 1],
        duration: 600,
        easing: 'easeOutExpo'
      })
    },
    hideGridItem(delay = 1200) {
      return anime({
        targets: this.$refs.gridItem,
        translateY: [0, 50],
        opacity: [0.4, 0],
        duration: 1000,
        delay: delay,
        easing: 'easeOutExpo'
      })
    },
    showGridItem() {
      return anime({
        targets: this.$refs.gridItem,
        translateY: [50, 0],
        opacity: [0, 0.4],
        duration: 1000,
        easing: 'easeOutExpo'
      })
    },
    showProductsInfos(delay = 1500) {
      return anime({
        targets: this.$refs.productInfos,
        opacity: [0, 0.4],
        delay: 800,
        duration: 1500,
        easing: 'easeOutExpo'
      })
    },
    hideProductionInfos() {
      return anime({
        targets: this.$refs.productInfos,
        opacity: [0.4, 0],
        duration: 1500,
        easing: 'easeOutExpo'
      })
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.rowHeight = document.body.clientHeight / 2.5 + 'px'
      /**
       * @TODO 如果需要ipad 这里要计算 图片 rem
       */
    })
  }
}
</script>
<style scoped>
.grid_product_box {
  width: 90%;
  height: 100%;
  margin: 0 auto;
  overflow: hidden;
}
.products_gallery td {
  position: relative;
}
.products_gallery td img {
  height: 4.5rem;
  opacity: 0.4;
}
.products_gallery tr {
  height: 6.2rem;
}
.products_gallery {
  width: calc(100% + 3rem);
  margin-left: -1.5rem;
  margin-top: -3rem;
  height: 100%;
}
.product_infos {
  opacity: 0;
  position: absolute;
  top: 0;
}
/** touch_move **/
.touch_move {
  transform: translateX(45px) translateY(90px) scale(0);
  position: absolute;
  bottom: 0;
  right: 0;
}
/** touchScale **/
.touch_scale_bottom {
  position: absolute;
  bottom: 20%;
}

.touch_scale_top {
  position: absolute;
  right: 0;
  top: 20%;
}

.touch_product {
  position: absolute;
  right: 0;
}
</style>
