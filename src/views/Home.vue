<template>
  <div class="index-page">
    <top-header />
    <TopBar />
    <MenuBanner />
    <SubChannel />
    <div class="gray-page">
      <FlashSale/>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import TopHeader from "../components/TopHeader.vue";
import TopBar from "../components/TopBar";
import MenuBanner from "../components/MenuBanner.vue";
import SubChannel from "../components/SubChannel";
import FlashSale from '../components/FlashSale.vue';

export default {
  name: "Home",
  components: {
    TopHeader,
    TopBar,
    MenuBanner,
    SubChannel,
    FlashSale,
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
}
</style>
