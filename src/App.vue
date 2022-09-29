<template>
  <div id="app">
    <SlideTopCard />
    <Question
      v-if="current === 1"
      @end="hanledEnd"
    />
    <ResultPage v-if="current === 2"/>
  </div>
</template>

<script>
import Question from '@/components/QuestionList'
import ResultPage from '@/components/ResultPage'
import SlideTopCard from '@/components/SlideTopCard'
export default {
  name: 'App',
  components: {
    Question,
    ResultPage,
    SlideTopCard
  },
  data() {
    return {
      current: 1
    }
  },
  methods: {
    hanledEnd(res) {
      console.log(res)
      this.next()
    },
    next() {
      this.current += 1
    }
  }
}
</script>

<style lang="scss">
#app {
  position: relative;
  width: 100%;
  height: 100%;
}
</style>
