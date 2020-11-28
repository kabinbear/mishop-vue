<template>
  <div class="good-box">
    <div class="box-header">
      <h3 class="header-title">{{ goodsItem.boxTitle }}</h3>
      <div class="checkall" v-if="!goodsItem.isHot">
        <span>查看全部</span>
        <i class="fa fa-angle-right"> </i>
      </div>
      <ul class="Header-Tab" v-else>
        <li
          class="Tab-item"
          v-for="(item, index) in goodsItem.tabList"
          :key="index"
          :class="{ active: selectItem.type === item.type }"
          @mouseenter="selectType(item)"
        >
          {{ item.value }}
        </li>
      </ul>
    </div>
    <div class="box-content">
      <div class="promo-container">
        <div class="promo-one" v-if="goodsItem.listData.promo.length === 1">
          <a :href="goodsItem.listData.promo[0].url">
            <img :src="goodsItem.listData.promo[0].src" alt="" />
          </a>
        </div>
        <div class="promo-two" v-if="goodsItem.listData.promo.length === 2">
          <div
            class="promo-two-item"
            v-for="(item, index) in goodsItem.listData.promo"
            :key="index"
          >
            <a :href="item.url">
              <img :src="item.src" alt="" />
            </a>
          </div>
        </div>
      </div>

      <div class="goods-container">
        <div class="goods-one" v-if="!goodsItem.isHot">
          <div
            class="goods-item brick-item"
            v-for="(item, index) in goodsItem.listData.goods"
            :key="index"
          >
            <a :href="item.url"
              ><img :src="item.src" :alt="item.value" />
              <h3 class="name ellipsis">{{ item.value }}</h3>
              <span class="desc ellipsis">{{ item.desc }}</span>
              <div class="price">
                <span>{{ item.newPrice }}元</span>
                <span v-if="item.sub">起</span>
                <del v-if="item.oldPrice">{{ item.oldPrice }} 元</del>
              </div>
            </a>
          </div>
        </div>
        <div class="goods-item" v-else>
          <template v-for="(item, index) in goodsData">
            <div
              class="goods-item-sm"
              :key="index"
              v-if="
                index === goodsData.length - 1 && goodsData.length % 2 === 0
              "
            >
              <a class="brick-item" :href="item.url" target="_blank">
                <div class="text-container">
                  <h3 class="name">{{ item.value }}</h3>
                  <div class="price">
                    <span>{{ item.newPrice }}元</span>
                    <span v-if="item.sub">起</span>
                  </div>
                </div>
                <img :src="item.src" :alt="item.value" />
              </a>
              <a class="brick-more" :href="selectItem.url" target="_blank">
                <div class="text-container look-more">
                  <h3 class="name">浏览更多</h3>
                  <span class="desc">{{ selectItem.value }}</span>
                </div>
                <img src="../../assets/img/right.png" />
              </a>
            </div>
            <div
              class="goods-item-bg"
              :key="index"
              v-if="
                index === goodsData.length - 1 && goodsData.length % 2 !== 0
              "
            >
              <a class="brick-item" :href="item.url" target="_blank">
                <img :src="item.src" :alt="item.value" />
                <h3 class="name ellipsis">{{ item.value }}</h3>
                <span class="desc ellipsis">{{ item.desc }}</span>
                <div class="price">
                  <span>{{ item.newPrice }}元</span>
                  <span v-if="item.sub">起</span>
                  <del v-if="item.oldPrice">{{ item.oldPrice }}元</del>
                </div>
              </a>
              <a
                class="brick-more brick-item"
                :href="selectItem.url"
                target="_blank"
              >
                <div class="text-container look-more">
                  <h3 class="name">浏览更多</h3>
                  <span class="desc">{{ selectItem.value }}</span>
                </div>
                <img src="../../assets/img/right.png" />
              </a>
            </div>
            <div
              class="goods-item brick-item"
              :key="index"
              v-if="index < goodsData.length - 1"
            >
              <a :href="item.url" target="_blank">
                <img :src="item.src" :alt="item.value" />
                <h3 class="name ellipsis">{{ item.value }}</h3>
                <span class="desc ellipsis">{{ item.desc }}</span>
                <div class="price">
                  <span>{{ item.newPrice }}元</span>
                  <span v-if="item.sub">起</span>
                  <del v-if="item.oldPrice">{{ item.oldPrice }}元</del>
                </div>
              </a>
            </div>
          </template>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectItem: "",
      goodsData: "",
    };
  },
  methods: {
    selectType(item) {
      this.selectItem = item;
      this.goodsData = this.goodsItem.listData[item.type];
    },
    init() {
      if (this.goodsItem.tabList) {
        this.selectItem = this.goodsItem.tabList[0];
        this.goodsData = this.goodsItem.listData.hots;
      } else {
        this.selectItem = "";
        this.goodsData = "";
      }
    },
  },
  mounted() {
    this.init();
  },
  props: ["goodsItem"],
};
</script>

<style lang="scss">
.good-box {
  width: 1226px;
  margin: 0 auto;
  .box-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 57.6px;
    .checkall {
      span {
        display: inline-block;
      }
      i {
        background: #605751;
        width: 20px;
        height: 20px;
        color: #fff;
        transition: 0.4s all;
        border-radius: 15px;
        line-height: 20px;
        text-align: center;
        margin-left: 10px;
      }
      &:hover {
        span {
          color: #ff6700;
        }
        i {
          background: #ff6700;
        }
      }
    }
    .Header-Tab {
      display: flex;
      .Tab-item {
        margin-left: 30px;
        transition: all 0.5s;
        border: 2px solid transparent;
        &:hover {
          color: #ff6700;
          border-bottom: 2px solid #ff6700;
        }
      }
      .active {
        color: #ff6700;
        border-bottom: 2px solid #ff6700;
      }
    }
  }
  .box-content {
    display: flex;
    .promo-container .promo-one {
      a {
        display: block;
        height: 614px;
        img {
          height: 100%;
          width: 234px;
        }
      }
    }
    .promo-two-item {
      &:first-child {
        margin-bottom: 14px;
      }
      a {
        display: block;
        height: 300px;
        img {
          height: 100%;
          width: 234px;
        }
      }
    }

    .goods-container .goods-one,
    .goods-container .goods-item {
      width: 100%;
      display: flex;
      flex-wrap: wrap;
      .goods-item {
        background: #fff;
        height: 300px;
        width: 234px;
        margin-left: 14px;
        padding: 20px 0;
        margin-bottom: 14px;
        a {
          height: 248px;
          img {
            width: 160px;
            height: 160px;
          }
        }
        .text-container {
          .name {
            font-size: 14px;
            font-weight: 400;
            color: #333;
            margin: 0 10px 2px;
          }
          .desc {
            margin: 0 10px 14px;
          }
          .price {
            margin: 0 10px 14px;
            span {
              margin: 0 10px 14px;
              color: #ff6700;
              font-size: 14px;
            }
            del {
              color: #b0b0b0;
              margin-left: 8px;
            }
          }
        }
      }
      .goods-item-sm {
        background: #fff;
        height: 150px;
        width: 234px;
        margin-left: 14px;
        padding: 20px 0;
        margin-bottom: 14px;
        a {
          height: 248px;
          img {
            width: 160px;
            height: 160px;
          }
        }
        .name {
          font-size: 14px;
          font-weight: 400;
          color: #333;
          margin: 0 10px 2px;
        }
        .desc {
          margin: 0 10px 14px;
        }
        .price {
          margin: 0 10px 14px;
          span {
            margin: 0 10px 14px;
            color: #ff6700;
            font-size: 14px;
          }
          del {
            color: #b0b0b0;
            margin-left: 8px;
          }
        }
      }
      .tooew-item-bg{

      }
    }
  }
  .brick-item {
    transition: all 0.2s linear;
    &:hover {
      transform: translate3d(0, -2px, 0);
      box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
    }
  }
}
</style>