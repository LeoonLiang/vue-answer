<template>
  <div
    ref="SlideTopCard"
    class="slide-top-card"
    :style="{
      transform: `translateY(-${dis}px)`,
      transition: animateClass ? 'transform 0.2s' : ''
    }"
  >
  <span class="slide-tips">上滑</span>
  </div>
</template>

<script>
  export default {
    name: 'SlideTopCard',
    data() {
      return {
        startPosY: 0,
        endPosY: 0,
        dis: 0,
        animateClass: false
      }
    },
    mounted() {
      if (document.body.clientHeight > 800) {
        this.addMouseSlide()
      } else {
        this.addTouchSlide()
      }
    },
    methods: {
      addMouseSlide() {
        const dom = this.$refs.SlideTopCard
        dom.addEventListener('mousedown', this.mouseDown)
      },
      mouseDown(e) {
        const dom = this.$refs.SlideTopCard
        this.startPosY = e.pageY;
        dom.addEventListener('mousemove', this.mouseMove)
        dom.addEventListener('mouseup', this.mouseUp)
      },
      mouseMove(e) {
        this.endPosY = e.pageY;
        this.dis = this.startPosY - this.endPosY
      },
      mouseUp() {
        const dom = this.$refs.SlideTopCard
        dom.removeEventListener('mousemove', this.mouseMove)
        dom.removeEventListener('mouseup', this.mouseUp)
        this.touchEnd()
      },
      addTouchSlide() {
        const dom = this.$refs.SlideTopCard
        dom.addEventListener('touchstart', this.touchStart)
        dom.addEventListener('touchmove', this.touchMove)
        dom.addEventListener('touchend', this.touchEnd)
      },
      touchStart(e) {
        this.animateClass = false
        const touch = e.touches[0];
        this.startPosY = touch.pageY;
      },
      touchMove(e) {
        const touch = e.touches[0];
        this.endPosY = touch.pageY;
        this.dis = this.startPosY - this.endPosY
      },
      touchEnd() {
        this.animateClass = true
        const pageHeight = document.body.clientHeight
        if (this.dis > pageHeight / 2) {
          this.slideToTop()
        } else {
          this.slideToDown()
        }
      },
      slideToDown() {
        this.startPosY = 0
        this.endPosY = 0
        this.dis = 0
      },
      slideToTop() {
        const pageHeight = document.body.clientHeight
        this.startPosY = 0
        this.endPosY = 0
        this.dis = pageHeight
      }
    }
  }
</script>

<style lang="scss" scoped>
  .slide-top-card {
    width: 100%;
    height: 100vh;
    background-color: red;
    box-sizing: border-box;
    font-size: 16rem;
    position: relative;
  }
  .slide-tips {
    position: absolute;
    left: 50%;
    bottom: 20%;
    transform: translateX(-50%);
    font-size: 12rem;
  }
</style>