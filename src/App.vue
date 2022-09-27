<template>
  <div id="app">
    <SlideTopCard></SlideTopCard>
  </div>
</template>

<script>
import SlideTopCard from '@/components/SlideTopCard'
export default {
  name: 'App',
  components: {
    SlideTopCard
  }
}
</script>

<style lang="scss">
  .app {
    width: 100%;
    height: 100%;
  }
</style>
