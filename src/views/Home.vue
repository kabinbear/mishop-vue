<template>
  <div>
    <top-header />
    <TopBar />
    <MenuBanner />
    <SubChannel />
    <div class="gray-page">
      <div class="container">
        <FlashSale />
        <goods-sale></goods-sale>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import TopHeader from "../components/TopHeader.vue";
import TopBar from "../components/TopBar";
import MenuBanner from "../components/MenuBanner.vue";
import SubChannel from "../components/SubChannel";
import FlashSale from "../components/FlashSale.vue";
import GoodsSale from "../components/GoodsSale";

export default {
  name: "Home",
  components: {
    TopHeader,
    TopBar,
    MenuBanner,
    SubChannel,
    FlashSale,
    GoodsSale,
  },
};
</script>
<style lang="scss">
.gray-page {
  display: flex;
  flex-flow: column;
  width: 100%;
  height: auto;
  background: rgb(245, 245, 245);
  overflow: hidden;
}
.container {
  width: 1226px;
  margin-right: auto;
  margin-left: auto;
}
</style>
