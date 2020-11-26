<template>
  <header class="tophead">
    <div class="maxwidth">
      <!-- 内容nav -->
      <ul class="nav">
        <li v-for="(item, index) in navsData" :key="index" class="nav-item">
          <div class="item-style" v-if="item.value === '小米商城'">
            <a :href="item.url">{{ item.value }}</a>
          </div>
          <div class="item-style" v-if="item.value === 'Select Location'">
            <a :href="item.url">{{ item.value }} </a>
          </div>
          <div
            class="item-style"
            v-if="item.value === '下载app'"
            @mouseenter="downloadQRCodeShow"
            @mouseleave="downloadQRCodeHide"
          >
            <a target="_blank" :href="item.url" class="app-qrcode-container">
              {{ item.value }}
              <transition name="qrcode-trans">
                <div class="app-qrcode" v-show="downloadFlag">
                  <img
                    src="https://i1.mifile.cn/f/i/17/appdownload/download.png?1"
                    alt="小米商城"
                  />
                  <span>小米商城App</span>
                </div>
              </transition>
            </a>
            <!-- <span class="triangle" v-show="downloadFlag"></span> -->
          </div>
          <div
            class="item-style"
            v-if="
              item.value !== '小米商城' &&
              item.value !== '下载app' &&
              item.value !== 'Select Location'
            "
          >
            <a :href="item.url" target="_blank">{{ item.value }}</a>
          </div>
          <span class="navSpan" v-show="index !== navsData.length - 1">|</span>
        </li>
      </ul>
      <!-- 登录nav -->
      <div class="nav-login">
        <ul class="nav">
          <li v-for="(item, index) in loginData" :key="index" class="nav-item">
            <template v-if="item.value === '消息通知'">
              <a :href="item.url" style="margin-left: 5px">{{
                item.value
              }}</a></template
            >
            <template v-else>
              <a href="item.url" target="_blank">{{ item.value }}</a>
            </template>
            <span class="navSpan" v-show="index !== loginData.length - 1"
              >|</span
            >
          </li>
        </ul>
        <div class="cart" @mouseenter="cartListShow" @mouseleave="cartListHide">
          <div class="cart-container" :class="{ active: showFlag }">
            <i class="fa fa-shopping-cart icon-cart"></i>
            <a href="http://static.mi.com/cart/">
              购物车(
              <span>0</span>
              )
            </a>
          </div>
          <transition name="fade-in">
            <div class="cart-list" v-show="showFlag">
              <div class="cart-list-word">购物车中还没有商品，快去选购吧！</div>
            </div>
          </transition>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  data() {
    return {
      navsData: [
        { value: "小米商城", url: "https://www.mi.com/index.html" },
        { value: "MIUI", url: "https://www.miui.com/" },
        { value: "loT", url: "https://iot.mi.com/index.html" },
        { value: "云服务", url: "https://i.mi.com/" },
        { value: "金融", url: "https://jr.mi.com?from=micom" },
        { value: "有品", url: "https://youpin.mi.com/" },
        { value: "小爱开放平台", url: "https://xiaoai.mi.com/" },
        { value: "企业团购", url: "https://qiye.mi.com/" },
        { value: "资质证照", url: "https://www.mi.com/aptitude/list/?id=41" },
        { value: "协议规则", url: "https://www.mi.com/aptitude/list/" },
        { value: "下载app", url: "https://www.mi.com/appdownload/" },
        { value: "Select Location", url: "javascript:void(0);" },
      ],
      loginData: [
        {
          value: "登陆",
          url:
            "http://order.mi.com/site/login?redirectUrl=http://www.mi.com/index.html",
        },
        { value: "注册", url: "https://account.xiaomi.com/pass/register" },
        { value: "消息通知", url: "http://order.mi.com/message/list" },
      ],
      downloadFlag: false,
      showFlag: false,
    };
  },
  methods: {
    downloadQRCodeShow() {
      this.downloadFlag = true;
    },
    downloadQRCodeHide() {
      this.downloadFlag = false;
    },
    cartListShow() {
      this.showFlag = true;
    },
    cartListHide() {
      this.showFlag = false;
    },
  },
};
</script>

<style lang="scss">
.tophead {
  width: 100%;
  height: 40px;
  background-color: rgb(51, 51, 51);
  .maxwidth {
    width: 1226px;
    display: flex;
    justify-content: space-between;
    margin: 0 auto;
    .nav {
      display: flex;
      .nav-item {
        height: 40px;
        line-height: 40px;
        display: inline-block;
        position: relative;
        .item-style {
          display: inline-block;
          a {
            display: inline-block;
            font-size: 12px;
            color: #b0b0b0;
            line-height: 40px;
            text-decoration: none;
            &:hover {
              color: #ffffff;
            }
          }
        }
      }
      .app-qrcode-container {
        position: relative;
        display: inline-block;

        &:hover::before {
          content: "";
          position: absolute;
          bottom: 0;
          left: 50%;
          width: 0;
          height: 0;
          margin-left: -8px;
          border-width: 0 8px 8px;
          border-style: solid;
          border-color: transparent transparent #ffffff;
        }
        .app-qrcode {
          position: absolute;
          display: inline-block;
          background: #ffffff;
          top: 38px;
          left: -35px;
          width: 124px;
          box-shadow: 0 3px 3px #aaaaaa;
          overflow: hidden;
          img {
            display: block;
            margin: 18px auto 12px;
            width: 90px;
            height: 90px;
          }
          span {
            display: block;
            text-align: center;
            font-size: 14px;
            color: #333;
            line-height: 1;
            margin-bottom: 12px;
          }
        }
      }
      .navSpan {
        color: #424242;
        margin: 0 5px;
        line-height: 40px;
      }
    }
  }
}
.nav-login {
  display: flex;
  .nav-item {
    display: inline-block;
    a {
      display: inline-block;
      font-size: 12px;
      color: #b0b0b0;
      line-height: 40px;
      text-decoration: none;
      &:hover {
        color: #ffffff;
      }
    }
  }
  .cart {
    display: inline-block;
    width: 120px;
    background: #424242;
    height: 40px;
    line-height: 40px;
    margin-left: 25px;
    cursor: pointer;
    position: relative;
    .cart-container {
      line-height: 40px;
      i {
        font-size: 16px;
        color: #b0b0b0;
      }
      a {
        color: #b0b0b0;
        text-decoration: none;
        font-size: 14px;
        line-height: 40px;
        margin-left: 5px;
      }
    }
    .cart-list {
      position: absolute;
      background-color: #ffffff;
      box-shadow: 0 2px 10px rgba($color: #000000, $alpha: 0.3);
      width: 345px;
      height: 96px;
      right: 0;
      top: 40px;
      z-index: 99;
      overflow: hidden;
      .cart-list-word {
        text-align: center;
        color: black;
        height: 96px;
        line-height: 96px;
      }
    }
  }
}

.fade-in-enter-active,
.fade-in-leave-active {
  transition: all 0.2s ease;
  height: 96px;
}

.fade-in-enter,
.fade-in-leave-to {
  height: 0;
}

.fade-in-enter-to,
.fade-in-leave {
  height: 96px;
}

.qrcode-trans-enter-active,
.qrcode-trans-leave-active {
  transition: all 0.3s ease;
  height: 146px;
}

.qrcode-trans-enter,
.qrcode-trans-leave-to {
  height: 0;
}
.qrcode-trans-enter-to,
.qrcode-trans-leave {
  height: 146px;
}
</style>