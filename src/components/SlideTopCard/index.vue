<!-- 上滑封面 -->
<template>
  <div
    v-if="hide"
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
        animateClass: false,
        hide: true
      }
    },
    mounted() {
      if (window.innerWidth > 800) {
        this.addMouseSlide()
      } else {
        this.addTouchSlide()
      }
    },
    methods: {
      addMouseSlide() {
        const dom = this.$refs.SlideTopCard
        if (!dom) {
          return
        }
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
        if (!dom) {
          return
        }
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
        const pageHeight = window.innerHeight
        console.log(74, this.dis, pageHeight)
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
        const pageHeight = window.innerHeight
        this.startPosY = 0
        this.endPosY = 0
        this.dis = pageHeight
        
        setTimeout(() => {
          this.hide = false          
        }, 1000);
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
    cursor: grab;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 99;
  }
  .slide-tips {
    position: absolute;
    left: 50%;
    bottom: 20%;
    transform: translateX(-50%);
    font-size: 12rem;
    color: #FFF;
  }
</style>