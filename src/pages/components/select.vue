<template lang="html">
  <div :class="$style.container">
    <div :class="$style.item" @click="handleClick('综合排序')">
      <span>综合排序</span>
      <i :class="['iconfont', 'icon-bottom', $style.rightIcon]"></i>
    </div>
    <div :class="$style.item" @click="handleClick('距离最近')">
      <span>距离最近</span>
    </div>
    <div :class="$style.item" @click="handleClick('会员领红包')">
      <i :class="['iconfont', 'icon-huangguan', $style.leftIcon]"></i>
      <span>会员领红包</span>
    </div>
    <div :class="$style.item" @click="handleClick('筛选')">
      <span :class="$style.footerText">筛选</span>
      <i :class="['iconfont', 'icon-webicon20', $style.rightIcon]"></i>
    </div>

    <div :class="$style.borderLine">

    </div>
  </div>
</template>

<script>
export default {
  name: 'selectPage',
  methods: {
    handleClick (msg) {
      if (msg === '综合排序') {
        this.$emit('change', 1)
      } else if (msg === '距离最近') {
        console.log(msg)
        this.$emit('change', 2)
      } else if (msg === '会员领红包') {
        console.log(msg)
        this.$emit('change', 3)
      } else if (msg === '筛选') {
        console.log(msg)
        this.$emit('change', 4)
      }
    }
  }
}
</script>

<style lang="scss" module>
  .container {
    display: flex;
    flex: row;
    flex-direction: row;
    flex-wrap: nowrap;
    position: relative;
    .item {
      width: 168px;
      height: 68px;
      line-height: 68px;
      text-align: center;
      font-size: 24px;
      color: #666;
      .leftIcon {
        font-size: 24px;
        color: #fecb43;
        margin-left: -10px;
      }
      .rightIcon {
        color: #666;
        font-size: 24px;
      }
    }
    .borderLine {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      display: block;
      overflow: hidden;
      border: 1px solid #f5f5f5;
    }
  }
</style>
