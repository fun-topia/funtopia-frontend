<template>
  <el-dialog
    center
    top="0"
    :title="$t('approvePopup.text2') + '&' + operation.name"
    :visible="getApprovePopup"
    :modal-append-to-body="false"
    :close-on-click-modal="false"
    :destroy-on-close="true"
    @close="closePopup"
  >
    <div class="popupbox">
      <el-steps :active="popupActive" align-center>
        <el-step>
          <template slot="icon">
            <div class="normal_icon">
              <div class="icon1">
                <div><i class="iconfont pcshouquan"></i></div>
              </div>
            </div>
          </template>
          <template slot="description">
            <div class="normal_des active">
              <div class="title">{{ $t("approvePopup.text3") }}</div>
              <div class="status">
                <div>{{ popupActive == 1 ? $t("status.text10") : $t("status.text11") }}</div>
              </div>
              <el-button type="primary" :loading="approvedLoading" @click="toApprove" :disabled="popupActive == 2">
                {{ $t("approvePopup.text2") }}
              </el-button>
            </div>
          </template>
        </el-step>
        <el-step>
          <template slot="icon">
            <div class="normal_icon">
              <div class="icon2" :class="{ active: popupActive == 2 }">
                <div>
                  <div><i class="iconfont pcqianbao2-mianxing"></i></div>
                </div>
              </div>
            </div>
          </template>
          <template slot="description">
            <div class="normal_des">
              <div class="title">{{ $t("approvePopup.text4") }}</div>
              <div class="status">
                <div v-show="popupActive == 2">{{ $t("status.text10") }}</div>
              </div>
              <el-button type="primary" :disabled="popupActive == 1" :loading="loading" @click="toOperate">
                {{ operation.name }}
              </el-button>
            </div>
          </template>
        </el-step>
      </el-steps>
    </div>
  </el-dialog>
</template>

<script>
import { mapGetters } from "vuex";
export default {
  name: "ApprovePopup",
  computed: { ...mapGetters(["getApprovePopup"]) },
  props: ["operation", "loading"],
  data() {
    return {
      approvedLoading: false,
      popupActive: 1,
    };
  },

  methods: {
    async toApprove() {
      this.approvedLoading = true;
      try {
        //const tx = await erc20(token().USDT).connect(getSigner()).approve(token().CB, util.parseUnits((1e10).toString()));
        // const tx = await erc721(token().CN).connect(getSigner()).setApprovalForAll(contract().Market,true);
        await this.$parent.toApprove();
        // const etReceipt = await tx.wait();

        this.approvedLoading = false;
        this.popupActive = 2;
      } catch (err) {
        console.error("approve", err);
        this.approvedLoading = false;
        this.popupActive = 1;
      }
    },
    toBuy() {
      this.$parent.buyBoxes();
    },
    toOperate() {
      switch (this.operation.func) {
        case "sellNfts":
          this.$parent.sellNfts();
          break;
        case "buyBoxes":
          this.$parent.buyBoxes();
          break;
        case "buyNfts":
          this.$parent.buyNfts();
          break;
      }
      // this.isLoading = false;
    },
    closePopup() {
      this.$store.commit("setApprovePopup", false);
      this.popupActive = 1;
    },
  },
};
</script>

<style lang="scss" scoped>
/deep/ .el-step__main {
  margin-top: 0.2rem;
}
.popupbox {
  width: 4rem;
  padding: 0.3rem 0;
  .normal_icon {
    min-width: 0.5rem;
    min-height: 0.5rem;
    width: 0.5rem;
    height: 0.5rem;
    .icon1 {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      padding: 0.05rem;
      background: linear-gradient(90deg, rgba(68, 129, 157, 0.37) 0%, rgba(122, 100, 158, 0.37) 100%);
      > div {
        width: 100%;
        height: 100%;
        background: linear-gradient(90deg, #44819d 0%, #7a649e 100%);
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        i {
          font-size: 0.35rem;
          color: #ffffff;
        }
      }
    }
    .icon2 {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      padding: 0.02rem;
      background: #5b5b5b;
      > div {
        width: 100%;
        height: 100%;
        border-radius: 50%;
        padding: 0.02rem;
        background: #211f24;
        > div {
          width: 100%;
          height: 100%;
          border-radius: 50%;
          background: #5b5b5b;
          display: flex;
          align-items: center;
          justify-content: center;
          i {
            font-size: 0.35rem;
            color: #211f24;
          }
        }
      }
      &.active {
        background: linear-gradient(90deg, rgba(68, 129, 157, 0.37) 0%, rgba(122, 100, 158, 0.37) 100%);
        > div {
          > div {
            background: linear-gradient(90deg, #44819d 0%, #7a649e 100%);
            i {
              color: #ffffff;
            }
          }
        }
      }
    }
  }
  .normal_des {
    .title {
      font-size: 0.12rem;
      font-weight: bold;
      color: #ffffff;
    }
    .status {
      width: 1.2rem;
      height: 0.25rem;
      line-height: 0.25rem;
      margin: 0.1rem auto;
      > div {
        width: 100%;
        height: 100%;
        font-size: 0.12rem;
        font-weight: bold;
        color: #ffffff;
        background: linear-gradient(90deg, #44819d 0%, #7a649e 100%);
        border-radius: 0.04rem;
      }
    }
  }
}
.el-button {
  width: 1.2rem;
  height: 0.5rem;
  line-height: 0.5rem;
  font-size: 0.15rem;
}
@media screen and (max-width: 750px) {
  /deep/ .el-step__main {
    margin-top: 0.2rem;
  }
  .popupbox {
    width: 80vw;
    padding: 0.1rem 0;
    .normal_icon {
      min-width: 0.4rem;
      min-height: 0.4rem;
      width: 0.4rem;
      height: 0.4rem;
      .icon1 {
        > div {
          i {
            font-size: 0.2rem;
          }
        }
      }
      .icon2 {
        > div {
          > div {
            i {
              font-size: 0.2rem;
            }
          }
        }
      }
    }
    .normal_des {
      .title {
        font-size: 0.12rem;
        font-weight: bold;
      }
      .status {
        width: 1rem;
        height: 0.2rem;
        line-height: 0.2rem;
        margin: 0.05rem auto;
        > div {
          font-size: 0.12rem;
          font-weight: bold;
        }
      }
    }
  }
  .el-button {
    width: 1rem;
    height: 0.35rem;
    line-height: 0.35rem;
    font-size: 0.12rem;
  }
}
</style>
