<template>
  <div class="turntable">
    <img
      ref="turntableRef"
      :src="TurntableImg"
      class="wheel"
      :style="{
        transform: `rotate(${turnsNum * 360}deg)`,
        transitionDuration: `${duration}s`
      }"
    >
    <div class="pointer" @click="start(getRandom(0, 2))"></div>
  </div>
</template>
<script>
import TurntableImg from '@/assets/wheel.png'
import { getRandom } from '@/utils'
export default {
  name: 'TurntableComponent',
  props: {
    // 转盘数据配置
    turntableConfig: {
      type: Object,
      default: () => ({
        // 一等奖
        1: {
          label: '一等奖',
          value: [[-16, 16]]  // 值是一个范围，这样不会一直停在一个点
        },
        2: {
          label: '二等奖',
          value: [[50, 82]]
        },
        0: {
          label: '三等奖',
          value: [[17, 49], [178, 210], [242, 274]] // 多个值，可以当做很多相同选项，如多个谢谢惠顾
        }
      })
    },
    duration: {
      type: Number,
      default: 6.5
    }
  },
  data() {
    return {
      TurntableImg,
      // 基本圈数
      baseTurnNum: 6,
      // 旋转圈数
      turnsNum: 0,
      // 容错，尽量不停在边界
      dis: 8
    }
  },
  methods: {
    getRandom,
    start(resultIndex) {
      if (this.runnig) {
        alert('别急，抽奖中')
        return
      }
      this.runnig = true
      const resultObj = this.turntableConfig[resultIndex].value
      const randomArr = resultObj[getRandom(0, resultObj.length - 1)]
      const resultAngle = getRandom(randomArr[0] + this.dis, randomArr[1] - this.dis)
      this.turnsNum = Math.floor(this.turnsNum) + this.baseTurnNum - resultAngle / 360
      setTimeout(() => {
        this.runnig = false
        alert(`恭喜获得${this.turntableConfig[resultIndex].label}`)
      }, this.duration * 1000)
    }
  }
}
</script>

<style lang="scss" scoped>
  .turntable {
    position: relative;
    height: 200rem;
    width: 100%;
  }
  .wheel {
    width: 200rem;
    height: 200rem;
    position: absolute;
    left: 50%;
    top: 50%;
    margin-left: -100rem;
    margin-top: -100rem;
    transition: transform 6.5s;
  }
  .pointer {
    width: 4px;
    height: 50px;
    background-color: black;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    cursor: pointer;
    &::before {
      content: '';
      width: 10px;
      height: 10px;
      border: 4px solid black;
      border-right: none;
      border-bottom: none;
      transform: translateX(-50%) rotate(45deg);
      position: absolute;
      top: 0;
      left: 50%;
    }
  }
</style>