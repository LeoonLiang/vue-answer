<template>
  <div class="turntable">
    <img
      ref="wheelRef"
      :src="Wheel"
      class="wheel"
    >
    <div class="pointer">

    </div>
  </div>
</template>
<script>
import Wheel from '@/assets/wheel.png'
export default {
  name: 'TurntableComponent',
  data() {
    return {
      Wheel
    }
  },
  methods: {

  }
}
</script>

<style lang="scss">
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
  }
  .pointer {
    width: 10px;
    height: 50px;
    background-color: red;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
  }
</style>