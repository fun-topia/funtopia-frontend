<template>
  <div id="container" :class="isEnLang ? 'fontfamily_en' : 'fontfamily_zh'">
    <HeaderLayout />
    <div id="container_body">
      <router-view />
      <FooterLayout />
    </div>
    <el-backtop></el-backtop>
    <WalletListPopup></WalletListPopup>
    <WalletConnectPopup></WalletConnectPopup>
  </div>
</template>
<script>
import { mapGetters } from "vuex";
import HeaderLayout from "@/layout/HeaderLayout.vue";
import FooterLayout from "@/layout/FooterLayout.vue";
import WalletListPopup from "@/components/WalletListPopup.vue";
import WalletConnectPopup from "@/components/WalletConnectPopup.vue";

export default {
  components: { HeaderLayout, FooterLayout, WalletListPopup, WalletConnectPopup },
  data() {
    return {};
  },
  computed: { ...mapGetters(["isEnLang"]), ...mapGetters(["getWalletAccount"]) },
  mounted() {
    window.addEventListener("load", () => {
      this.resetRem();
    });
    window.addEventListener("resize", () => {
      this.resetRem();
    });
    this.$utils.addEventListenerFun();
  },
  beforeDestroy() {
    window.removeEventListener("load", this.resetRem());
    window.removeEventListener("resize", this.resetRem());
  },
  methods: {
    resetRem() {
      const clientWidth = document.body.clientWidth;
      let rem = 0;
      if (1440 <= clientWidth) {
        rem = 100;
      } else if (750 < clientWidth && clientWidth < 1440) {
        rem = (clientWidth * 100) / 1440;
      } else if (clientWidth <= 750) {
        rem = (clientWidth * 100) / 375;
      }
      document.getElementsByTagName("html")[0].style.fontSize = rem + "px";
    },
  },
};
</script>

<style lang="scss">
@media screen and (max-width: 750px) {
  #container {
    #container_body {
      padding-bottom: 0.6rem;
    }
  }
}
</style>
