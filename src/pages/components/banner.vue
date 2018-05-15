<template lang="html">
  <div :class="$style.container">
    <div :class="$style.header">
      <div :class="$style.left">
        {{leftText}}
      </div>
      <div :class="$style.right">
        {{rightText}}
        <i :class="['iconfont', 'icon-right', $style.more]"></i>
      </div>
    </div>
    <ul :class="$style.list">
      <li v-for="(item, index) in lists" :key="item.text" :class="index !== (lists.length -1) ? $style.distance: '' ">
        <img :src="item.img" />
        <h4>{{item.title}}</h4>
        <p>{{item.text}}</p>
        <div :class="$style.info">
          <span :class="$style.price">{{item.price}}</span>
          <span :class="$style.num" v-if="item.num">{{item.num}}</span>
          <span :class="$style.desc" v-else>{{item.desc}}</span>
        </div>
      </li>
    </ul>
    <section :class="$style.footer">
      <Select @change="handleChangeEmit"/>
    </section>

    <!-- tab1的弹窗 -->
    <div :class="$style.layer" v-if="istab1">
      <section :class="$style.content">
        <Select @change="handleChangeEmit"/>
        <ul>
          <li v-for="(item, index) in textItems" :key="item.text" @click="handleSelectNumClick(index)">
            <span :class="index === selectedNum ? $style.select: '' ">{{item.text}}</span>
            <i :class="['iconfont', 'icon-duihao', $style.select]" v-if="index === selectedNum"></i>
          </li>
        </ul>
      </section>
    </div>

    <!-- tab4的弹窗 -->
    <section :class="$style.layer" v-if="istab4">
      <div :class="$style.content">
        <div :class="$style.tab4Title">
          配送方式
        </div>
        <div :class="$style.mode">
          <div :class="$style.modeItem">
            <span>蜂鸟专送</span>
          </div>
        </div>

        <div :class="$style.tab4Title">
          优惠活动
        </div>

        <div :class="$style.mode">
          <div :class="$style.modeItem">
            <span :class="$style.font" style="background:#70bc46;color:#fff;">新</span>
            <span>新用户优惠</span>
          </div>
          <div :class="$style.modeItem">
            <span :class="$style.font" style="background:#f1884f;color:#fff;">特</span>
            <span>特价商品</span>
          </div>
          <div :class="$style.modeItem">
            <span :class="$style.font" style="background:#f07373;color:#fff;">减</span>
            <span>下拉立减</span>
          </div>
          <div :class="$style.modeItem">
            <span :class="$style.font" style="background:#3cc791;color:#fff;">赠</span>
            <span>赠品优惠</span>
          </div>
          <div :class="$style.modeItem">
            <span :class="$style.font" style="background:#ff7239;color:#fff;">返</span>
            <span>下单返红包</span>
          </div>
          <div :class="$style.modeItem">
            <span :class="$style.font" style="background:#ffac2a;color:#fff;">领</span>
            <span>进店领红包</span>
          </div>
        </div>

        <div :class="$style.tab4Title">
          人均消费
        </div>

        <div :class="$style.mode">
          <div :class="$style.modeItem">
            <span>￥20以下</span>
          </div>
          <div :class="$style.modeItem">
            <span>￥20~40</span>
          </div>
          <div :class="$style.modeItem">
            <span>￥40以上</span>
          </div>
        </div>

        <div :class="$style.tab4Title">
          商家属性(可多选)
        </div>

        <div :class="$style.mode">
          <div :class="$style.modeItem">
            <span :class="$style.font" style="color:#3fbde6;border:1px solid #3fbde6;border-radius:3px;">品</span>
            <span>品牌商家</span>
          </div>
          <div :class="$style.modeItem">
            <span :class="$style.font" style="color:#999999;border:1px solid #999999;border-radius:3px;">保</span>
            <span>食安保</span>
          </div>
          <div :class="$style.modeItem">
            <span :class="$style.font" style="color:#e8842d;border:1px solid #e8842d;border-radius:3px;">新</span>
            <span>新店</span>
          </div>
          <div :class="$style.modeItem">
            <span :class="$style.font" style="color:#999999;border:1px solid #999999;border-radius:3px;">票</span>
            <span>开发票</span>
          </div>
          <div :class="$style.modeItem">
            <span :class="$style.font" style="color:#ff4e00;border:1px solid #ff4e00;border-radius:3px;">付</span>
            <span>在线支付</span>
          </div>
        </div>

        <div :class="$style.tab4Title" style="padding-bottom:0">
        </div>

        <div :class="$style.mode">
          <div :class="$style.btn">
            <span :class="$style.leftBtn">清空</span>
          </div>
          <div :class="$style.btn">
            <span :class="$style.rightBtn" @click="handleConfirmClick">确定</span>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import Select from './select.vue'
export default {
  name: 'banner',
  props: {
    lists: {
      type: Array,
      default: () => {
        return []
      }
    }
  },
  data () {
    return {
      leftText: '品质套餐',
      rightText: '更多',
      selectedNum: 0,
      textItems: [{
        text: '综合排序'
      },
      {
        text: '销量最高'
      },
      {
        text: '起送价最低'
      },
      {
        text: '配送最快'
      }],
      istab1: false,
      istab4: false
    }
  },
  components: {
    Select
  },
  methods: {
    handleSelectNumClick (index) {
      this.selectedNum = index
    },
    handleChangeEmit (data) {
      if (this.istab1 || this.istab4) {
        this.istab1 = this.istab1 ? !this.istab1 : this.istab1
        this.istab4 = this.istab4 ? !this.istab4 : this.istab4
      } else {
        if (data === 1) {
          this.istab1 = true
        } else if (data === 4) {
          this.istab4 = true
        }
      }
    },
    handleConfirmClick () {
      this.istab4 = false
    }
  }
}
</script>

<style lang="scss" module>
.container {
    position: relative;
    padding: 160px  17px 0 17px;
    box-sizing: border-box;
    .header {
        position: relative;
        height: 32px;
        line-height: 32px;
        .left {
            position: absolute;
            top: 0;
            left: 0;
            color: #333;
            font-size: 27px;
        }
        .right {
            position: absolute;
            top: 0;
            right: 0;
            color: #666;
            font-size: 20px;
        }
        .more {
            color: #666;
            font-size: 20px;
        }
    }
    .list {
        margin-top: 13px;
        display: flex;
        flex: row;
        flex-wrap: nowrap;
        img {
            width: 187px;
        }
        h4 {
            margin-top: 10px;
            width: 187px;
            color: #333;
            font-size: 24px;
            white-space: nowrap;
            text-overflow: ellipsis;
            overflow: hidden;
        }
        p {
            margin-top: 10px;
            color: #999;
            font-size: 20px;
        }
        .info {
            width: 187px;
            .price {
                color: #333;
                font-size: 22px;
                font-weight: bold;
            }
            .num {
                color: #999;
                font-size: 18px;
            }
            .desc {
                color: #e8470b;
                font-size: 18px;
                border: 1px solid #e8470b;
                padding: 2px 4px;
                box-sizing: border-box;
            }

        }
        .distance {
            margin-right: 20px;
        }
    }
    .layer {
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        height: 993px;
        z-index:100;
        background: rgba(0,0,0,.5);
        .content {
            background: #fff;
            ul {
                padding-left: 35px;
                padding-top: 13px;
                padding-bottom: 20px;
                box-sizing: border-box;
                li {
                    font-size: 24px;
                    height: 68px;
                    line-height: 68px;
                    > span {
                        display: inline-block;
                        width: 550px;
                    }
                    .select {
                        font-size: 24px;
                        color: #3190e8;
                    }
                }
            }
            .tab4Title {
                padding-left: 25px;
                padding-top: 17px;
                padding-bottom: 17px;
                box-sizing: border-box;
                font-size: 24px;
                color: #666;
                background: #fafafa;
                border:1px solid #f2f2f2;
            }
            .mode {
              display: flex;
              flex-direction: row;
              flex-wrap: wrap;
              border-radius: 1px solid #f2f2f2;
              .modeItem {
                width: 33.33333%;
                border:1px solid #f2f2f2;
                color:#333;
                font-size: 22px;
                padding-top: 17px;
                padding-bottom: 17px;
                padding-left: 40px;
                box-sizing: border-box;
                .font {
                  vertical-align: middle;
                  font-size:14px;
                  padding:3px 5px;
                }
              }
              .btn {
                width: 50%;
                font-size: 27px;
                height: 73px;
                line-height: 73px;
                text-align: center;
                .leftBtn {
                  display: inline-block;
                  background: #fff;
                  color: #ddd;
                  height: 73px;
                  width: 340px;
                  border: 1px solid #f2f2f2;
                }
                .rightBtn {
                  display: inline-block;
                  background: #00d762;
                  color: #fff;
                  height: 73px;
                  width: 340px;
                  border: 1px solid #f2f2f2;
                }
              }
            }
        }
    }
}
</style>
