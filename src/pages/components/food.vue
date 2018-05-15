<template lang="html">
  <div :class="$style.container">
    <ul>
      <li v-for="(item) in foods" :key="item.title" :class="$style.item">
        <div :class="$style.left">
          <img :src="item.img"/>
        </div>

        <div :class="$style.right">
          <div :class="$style.firstLine">
            <span>{{item.title}}</span>
            <span :class="$style.keyword"><em v-for="(item) in item.keyWords" :key="item" >{{item}}</em></span>
          </div>
          <div :class="$style.secondLine">
            <div :class="$style.stars">
              <i v-for="(itemA, index) in 5" :key="index" class="iconfont icon-star1" :class="index < item.starCount ? $style.star : $style.starFont "></i>
            </div>
            <span :class="$style.starCount">{{item.starCount}}</span>
            <span :class="$style.desc">{{item.desc}}</span>
          </div>
          <div :class="$style.thirdLine">
            <span>{{item.startSend}}</span>
            <span>{{item.discount}}</span>
            <div :class="$style.thirdLineRight">
              <span>{{item.distance}} &nbsp;|</span>
              <span>{{item.time}}</span>
            </div>
          </div>
          <ul :class="$style.fourLine">
            <li v-for="(itemB, index) in item.list" :key="index">
              <span v-if="itemB.title === '首'" style="background:#70bc46">{{itemB.title}}</span>
              <span v-else-if="itemB ==='减'" style="background:#f07373">{{itemB.title}}</span>
              <span v-else>{{itemB.title}}</span>
              <span>{{itemB.desc}}</span>
            </li>
            <div :class="$style.arrow" @click="item.isTop = !item.isTop">
              <span v-if="item.list.length > 0">{{item.list.length}}个活动</span>
              <i :class="['iconfont', 'icon-yooxi', $style.arrowTop]" v-if="item.isTop"></i>
              <i :class="['iconfont', 'icon-bottom', $style.arrowBottom]" v-else></i>
            </div>
          </ul>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'food',
  props: {
    foods: {
      type: Array,
      default: () => {
        return []
      }
    }
  }
}
</script>

<style lang="scss" module>
  .container {
    >ul {
      .item {
        padding: 40px 17px;
        box-sizing: border-box;
        display: flex;
        flex: row;
        flex-direction: row;
        flex-wrap: nowrap;
        border-bottom: 1px solid #eee;
        .left {
          width: 110px;
          height: 110px;
          img {
            width: 108px;
            height: 108px;
            border:1px solid #ddd;
          }
        }
        .right {
          padding-left: 10px;
          width: 477px;
          .firstLine {
            position: relative;
            height: 36px;
            line-height: 36px;
            font-size: 25px;
            font-weight: bold;
            color: #666;
            .keyword {
              position: absolute;
              top: 0;
              right: 10px;
              em {
                font-size: 18px;
                color:#999;
                margin-right: 10px;
                padding-left: 3px;
                padding-right: 3px;
                border: 1px solid #ddd;
              }
            }
          }
          .secondLine {
            margin-top: 15px;
            display: flex;
            flex-direction: row;
            flex-wrap: nowrap;
            .stars {
              display: flex;
              flex-direction: row;
              flex-wrap: nowrap;
              .star {
                font-size: 20px;
                color: #fecb43;
              }
              .starFont {
                font-size: 20px;
                color: #ddd;
              }
            }
            .starCount {
              margin-left: 10px;
              font-size: 18px;
              color: #666;
            }
            .desc {
              margin-left: 10px;
              font-size: 18px;
              color: #666;
            }
          }
          .thirdLine {
            position: relative;
            margin-top: 20px;
            display: flex;
            flex-direction: row;
            flex-wrap: nowrap;
            font-size: 18px;
            color: #666;
            span:nth-child(2) {
              margin-left: 10px;
            }
            .thirdLineRight {
              position: absolute;
              right: 0;
              top: 0;
              color: #999;
            }
          }
          .fourLine {
            margin-top: 40px;
            position: relative;
            li {
              display: flex;
              flex-direction: row;
              flex-wrap: nowrap;
              margin-top: 10px;
              span:nth-child(1) {
                display: inline-block;
                background: #f1884f;
                font-size: 20px;
                color: #fff;
                width: 28px;
                height: 28px;
                line-height: 28px;
                text-align: center;
              }
              span:nth-child(2) {
                margin-left: 10px;
                line-height: 30px;
                font-size: 18px;
                color: #666;
                text-overflow: ellipsis;
                overflow: hidden;
                white-space: nowrap;
              }
            }
            .arrow {
              position: absolute;
              right: 10px;
              top: -10px;
              >span {
                color: #999;
                font-size: 18px;
              }
            }
          }
        }
      }
    }
  }
</style>
