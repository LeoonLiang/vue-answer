<template>
  <div id="app">
    <Question
      v-if="current === 1"
      @end="hanledEnd"
    ></Question>
    <ResultPage v-if="current === 0"></ResultPage>
  </div>
</template>

<script>
import Question from '@/components/QuestionList'
import ResultPage from '@/components/ResultPage'
export default {
  name: 'App',
  components: {
    Question,
    ResultPage
  },
  data() {
    return {
      current: 0
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
