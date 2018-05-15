<template lang="html">
  <div :class="$style.container">
      <div :class="$style.text">
        {{text}}
      </div>
      <i :class="['iconfont', 'icon-left', $style.back]"></i>
  </div>
</template>

<script>
export default {
  name: 'homeHeader',
  data () {
    return {
      text: '美食'
    }
  }
}
</script>

<style lang="scss" module>
  .container {
    position: relative;
    height: 75px;
    width:640px;
    line-height: 75px;
    background: #008dfe;
    .back {
      position: absolute;
      left: 0;
      top: 0;
      color: #fff;
      font-size: 55px;
    }
    .text {
      text-align: center;
      color: #fff;
      font-size: 30px;
    }
  }
</style>
