<template>
  <div class="banner">
    <div class="banner-prev" @click="prev"></div>
    <div class="banner-next" @click="next"></div>
    <transition-group tag="ul" name="banner-trans" class="banner-container">
      <li
        class="image-container"
        v-for="item in banners"
        :key="item.key"
        v-show="item.key - 1 === imgIndex"
      >
        <!-- 为什么最好不要在transitionGroup 里使用 key 和 index ？ -->
        <a :href="item.url" target="_blank">
          <img :src="item.src" />
        </a>
      </li>
    </transition-group>
    <div class="banner-points">
      <a
        class="banner-point"
        @click="jump(index)"
        :class="{ active: index === imgIndex }"
        v-for="(item, index) in banners.length"
        :key="index"
      >
      </a>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      imgIndex: 0,
      timer:''
    };
  },
  props: ["banners"],
  methods: {
    prev() {
      const lastPage = this.banners.length - 1;
      if (this.imgIndex > 0) {
        this.imgIndex -= 1;
      } else {
        this.imgIndex = lastPage;
        //当imgIndex为0 也就是最开始 则直接跳到最后一个
      }
    },
    next() {
      const lastPage = this.banners.length - 1;
      if (this.imgIndex < lastPage) {
        this.imgIndex += 1;
      } else {
        this.imgIndex = 0;
        //当ImgIndex 等于最后一个时 跳到最开始
      }
    },
    jump(index) {
      this.imgIndex = index;
    },
    play(){
      clearInterval(this.timer);
      this.timer =  setInterval(()=>{
         this.next()
      },5000)
    }
  },
  mounted() {
    this.play()
  },
};
</script>

<style lang="scss">
.banner {
  position: relative;
  .banner-prev {
    position: absolute;
    background: url("../../assets/img/icon-slides.png") no-repeat -84px 50%;
    left: 234px;
    right: auto;
    top: calc(50% - 20px);
    cursor: pointer;
    z-index: 15;
    width: 41px;
    height: 69px;
    &:hover {
      background: url("../../assets/img/icon-slides.png") no-repeat 0px 50%;
    }
  }
  .banner-next {
    position: absolute;
    background: url("../../assets/img/icon-slides.png") no-repeat -126px 50%;
    left: auto;
    right: 0px;
    top: calc(50% - 20px);
    cursor: pointer;
    z-index: 15;
    width: 41px;
    height: 69px;
    &:hover {
      background: url("../../assets/img/icon-slides.png") no-repeat -42px 50%;
    }
  }

  .banner-container {
    width: 100%;
    height: 460px;
    overflow: hidden;
    .image-container {
      width: 100%;
      height: auto;
      a {
        display: block;
        img {
          width: 100%;
        }
      }
    }
  }
  .banner-points {
    position: absolute;
    display: flex;
    width: 150px;
    right: -30px;
    left: auto;
    bottom: 20px;
    z-index: 10;
    .banner-point {
      display: inline-block;
      width: 10px;
      height: 10px;
      border: 2px solid #fff;
      background: rgba(0, 0, 0, 0.4);
      margin: 0 4px;
      cursor: pointer;
      opacity: 1;
      border-radius: 50%;
      &:hover {
        background: hsla(0, 0, 100%, 0.4);
        border-color: rgba(0, 0, 0, 0.4);
      }
    }
    .active {
      background: hsla(0, 0, 100%, 0.4);
      border-color: rgba(0, 0, 0, 0.4);
    }
  }
}

.banner-trans-enter-active {
  transition: all 0.1s ease-in-out;
  opacity: 1;
}
.banner-trans-leave-active {
  opacity: 0;
}
.banner-trans-enter-to,
.banner-trans-leave {
  opacity: 1;
}
.banner-trans-enter,
.banner-trans-leave-to {
  opacity: 0;
}
</style>