<template>
  <div class="question-list">
    <div
      v-for="(item, index) in questionList"
      :key="index"
      class="question-item"
      :class="{
        read: result.length > index,
        active: current === index
      }"
      :style="{
        zIndex: questionList.length - index
      }"
    >
      <div>{{ item.title }}</div>
      <div class="choose-options">
        <div
          v-for="itm in optionsList"
          :key="itm.value"
          class="choose-options-item"
          @click="chooseAnswer(index, itm)"
        >
          {{ itm.label }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const optionsList = [
  {
    label: '同意',
    value: 'yes',
  },
  {
    label: '一般',
    value: 'normal'
  },
  {
    label: '反对',
    value: 'no'
  }
]
export default {
  name: 'QuestionList',
  props: {
    questionList: {
      type: Array,
      default() {
        return [
          {
            title: '题目1'
          },
          {
            title: '题目2'
          },
          {
            title: '题目3'
          },
          {
            title: '题目4'
          },
          {
            title: '题目5'
          }
        ]
      }
    }
  },
  data() {
    return {
      current: 0,
      result: [],
      optionsList
    }
  },
  computed: {
    isLast() {
      return this.current === this.questionList.length - 1
    }
  },
  methods: {
    chooseAnswer(index, item) {
      this.result[index] = item.value
      if (this.isLast) {
        this.$emit('end', this.result)
      } else {
        this.current = this.current + 1
      }
    }
  }
}
</script>

<style lang="scss" scoped>
  .question-list {
    padding-top: 100px;
    height: 200rem;
    overflow: hidden;
    position: relative;
  }
  .question-item {
    width: 300rem;
    margin: 0 auto;
    padding: 12rem;
    box-sizing: border-box;
    border-radius: 8rem;
    height: 200rem;
    transition: all 0.5s;
    position: absolute;
    left: 50%;
    top: 50%;
    margin-left: -150rem;
    background-color: #fff;
    margin-top: -100rem;
    z-index: 0;
    transform: scaleX(90%) translateY(3%);
    &:last-child {
      box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.04), 0px 4px 8px rgba(0, 0, 0, 0.06);
    }
    &.active {
      // z-index: 1;
      box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.04), 0px 4px 8px rgba(0, 0, 0, 0.06);
      transform: scale(1) translateY(0);
    }
    &.read {
      transform: translateY(-100%);
      opacity: 0;
      z-index: 2;
    }
  }
  .choose-options-item {
    font-size: 12rem;
    cursor: pointer;
  }
</style>