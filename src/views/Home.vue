<template>
  <div class="home">
    <top-header />
    <TopBar/>
    <MenuBanner/>
    <SubChannel/>
  </div>
</template>

<script>
// @ is an alias to /src
import TopHeader from "../components/TopHeader.vue";
import TopBar from '../components/TopBar'
import MenuBanner from '../components/MenuBanner.vue';
import SubChannel from '../components/SubChannel'
export default {
  name: "Home",
  components: {
    TopHeader,
    TopBar,
    MenuBanner
  },
};
</script>
