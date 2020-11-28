<template>
  <div class="swiper-box">
    <ul class="swiper" :style="transformStyle">
      <li
        class="swiper-item"
        v-for="(item, index) in slideItems"
        :key="index"
        :style="{ 'border-top-color': item.topColor }"
      >
        <a :href="item.url">
          <img :src="item.src" alt="" />
          <h3 class="item-name ellipsis">{{ item.value }}</h3>
          <div class="item-desc ellipsis">{{ item.desc }}</div>
          <div class="item-price">
            <span class="newprice">{{ item.newPrice }}元</span>
            <span class="oldprice">{{ item.oldPrice }}元</span>
          </div></a
        >
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["slideItems"],
  data() {
    return {
      Xvalue: 0,
      slideIndex: 0,
      slideTimer: "",
    };
  },
  methods: {
    //变化一下的轮播 x移动的992 = 盒子整体978 + 右margin 14px = 992pX
    //考虑到数据可能不是4的倍数 就多添加了一行
    next() {
      const lastindex = parseInt(this.slideItems.length / 4);
      if (this.slideIndex < lastindex) {
        if (
          this.slideIndex === lastindex - 1 &&
          this.slideItems.length % 4 !== 0
        ) {
          this.slideIndex += 1;
          this.Xvalue = -(
            (this.slideIndex - 1) * 992 +
            (this.slidItems.length % 4) * 248
          );
        } else {
          this.slideIndex += 1;
          this.Xvalue = -(this.slideIndex * 992);
        }
      } else {
        this.slideIndex = 0;
        this.Xvalue = 0;
      }
    },
    prev() {
      const lastindex = parseInt(this.slidItems.length / 4);
      if (this.slideIndex > 0) {
        this.slideIndex -= 1;
        this.Xvalue = -(this.slideIndex * 992);
      } else {
        this.slideIndex = lastIndex;
        this.Xvalue = -(lastIndex * 992);
      }
    },
    play() {
      clearInterval(this.slideTimer);
      this.slideTimer = setInterval(() => {
        this.next();
      }, 5000);
    },
  },
  computed: {
    transformStyle() {
      return {
        transform: `translate3d(${this.Xvalue}px,0,0)`,
      };
    },
  },
  mounted() {
    this.play();
  },
};
</script>

<style lang="scss" scoped>
.swiper-box {
  display: flex;
  width: 978px;
  height: 340px;
  margin-left: 14px;
  overflow: hidden;
  .swiper {
    height: 340px;
    display: flex;
    transition: all 1s ease-in-out;
    .swiper-item {
      width: 234px;
      height: 340px;
      background: #fff;
      padding-top: 30px;
      margin-right: 14px;
      border-top-width: 1px;
      border-top-style: solid;
      img {
        width: 160px;
        height: 160px;
        margin: 0 37px 22px;
      }
      .item-name {
        font-size: 15px;
        margin: 0 20px 3px;
        font-weight: 400;
        color: #212121;
      }

      .item-desc {
        color: rgb(176, 176, 176);
        font-size: 13px;
      }
      .item-price {
        text-align: center;
        padding-top: 10px;
        .newprice {
          color: rgb(255, 117, 31);
          margin: 0 5px;
        }
        .oldprice {
          color: rgb(176, 176, 176);
          text-decoration: line-through;
        }
      }
    }
  }
  .ellipsis {
    text-align: center;
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
  }
}
</style>