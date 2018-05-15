<template lang="html">
  <div :class="$style.container">
      <div :class="$style.header">
        <HomeHeader/>
        <SubHomeHeader :lists="subTitle"/>
      </div>
      <div :class="$style.body" ref="content">
        <div>
          <Banner :lists="lists"/>
          <Food :foods="foods"/>
        </div>
      </div>

  </div>
</template>

<script>
import http from '../service/APIServer'
import BScroll from 'better-scroll'
import HomeHeader from './components/header.vue'
import SubHomeHeader from './components/subHeader.vue'
import Banner from './components/banner.vue'
import Food from './components/food.vue'
export default {
  name: 'home',
  data () {
    return {
      subTitle: [],
      lists: [],
      foods: []
    }
  },
  components: {
    HomeHeader,
    SubHomeHeader,
    Banner,
    Food
  },
  created () {
    this.init()
  },
  mounted () {
    let content = this.$refs.content
    /* eslint-disable no-new */
    new BScroll(content, {
      scrollY: true,
      click: true
    })
  },
  methods: {
    async init () {
      let res = await http.get('/api/mock/index.json')
      if (res.code === 0) {
        this.subTitle = res.data.subTitle
        this.lists = res.data.lists
        this.foods = res.data.foods
      }
    }
  }
}
</script>

<style lang="scss" module>
  .container {
    .header {
      position: fixed;
      z-index: 100;
    }
    .body {
      height:100vh;
      overflow: hidden;
    }
  }
</style>
