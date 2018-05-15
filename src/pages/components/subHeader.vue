<template lang="html">
  <div :class="$style.container" ref="wrapper">
    <ul :class="$style.list">
      <li v-for="(item) in lists" :key="item.text" :class="$style.item">
        {{item.text}}
      </li>
    </ul>
  </div>
</template>

<script>
import BScroll from 'better-scroll'
export default {
  name: 'subHeader',
  props: {
    lists: {
      type: Array,
      default: () => {
        return []
      }
    }
  },
  mounted () {
    let wrapper = this.$refs.wrapper
    /* eslint-disable no-new */
    new BScroll(wrapper, {
      scrollX: true,
      click: true
    })
  }
}
</script>

<style lang="scss" module>
  .container {
    height: 68px;
    background: #008cfe;
    width: 100vw;
    overflow: hidden;
    .list {
      height:68px;
      line-height: 68px;
      padding: 0 10px;
      overflow: hidden;
      width: 640px;
      .item {
        float: left;
        color: #fff;
        padding: 0 20px;
        box-sizing: border-box;
        font-size: 24px;
      }
    }
  }
</style>
