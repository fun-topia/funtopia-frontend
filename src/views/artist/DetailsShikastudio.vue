<template>
  <div class="page">
    <div class="banner">
      <div class="back_box">
        <div @click="goBack">
          <i class="iconfont pcfanhui"></i><span>{{ $t("btns.text1") }}</span>
        </div>
      </div>
    </div>
    <div class="content">
      <div class="leftbox">
        <div class="cardbox">
          <img :src="card.card" alt="" />
          <span>{{ $t(card.name) }}</span>
          <div class="level_btn" :class="card.rarity" @click="openVideo">{{ $t("artist.text11") }}</div>
        </div>
        <div class="workbox">
          <div class="titlebtn">
            <div>
              <i class="iconfont pcintegral-fill"></i>
              {{ $t("artist.text4") }}
            </div>
          </div>
          <div class="text">
            <div>
              <pre>{{ $t(card.worddes) }}</pre>
            </div>
          </div>
        </div>
      </div>
      <div class="rightbox">
        <div :style="{ backgroundImage: `url(${card.card2})` }">
          <ul class="introbox1">
            <li>{{ $t(card.name) }}</li>
            <li>
              <div><i class="iconfont pcshuxingchaxun"></i>{{ $t("artist.text5") }}</div>
              {{ $t(card.attribute) }}
            </li>
            <li>
              <div><i class="iconfont pcpingfendengjiRating11"></i>{{ $t("artist.text6") }}</div>
              {{ $t(card.level) }}
            </li>
            <li>
              <div><i class="iconfont pcpingfendengjiRating15"></i>{{ $t("artist.text7") }}</div>
              {{ $t(card.starlevel) }}
            </li>
            <li>
              <div><i class="iconfont pcdengji"></i>{{ $t("artist.text8") }}</div>
              {{ card.rarity }}
            </li>
          </ul>
          <div class="introbox2">
            <div class="title">{{ $t("artist.text9") }}</div>
            <div class="text">
              <div>
                <pre>{{ $t(card.nftdes) }}</pre>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <el-dialog center top="0" :title="$t(card.name)" :visible.sync="isShowPopup" :modal-append-to-body="false" :destroy-on-close="true">
      <PaintingVideo :videoUrl="card.video"></PaintingVideo>
    </el-dialog>
  </div>
</template>

<script>
import PaintingVideo from "@/components/PaintingVideo.vue";
import { shikastudio } from "@/mock/nftworks";
export default {
  name: "DetailsShikastudio",
  components: { PaintingVideo },
  data() {
    return {
      card: null,
      isShowPopup: false,
    };
  },
  created() {
    if (Object.keys(this.$route.query).length > 0) {
      const id = this.$route.query.id;
      this.card = shikastudio.works.find((item) => item.id == id);
    }
  },
  methods: {
    openVideo() {
      this.isShowPopup = true;
    },
    goBack() {
      history.go(-1);
    },
  },
};
</script>

<style lang="scss" scoped>
.page {
  width: 100%;
  padding-top: 0.8rem;
}
.banner {
  width: 100%;
  height: 1rem;
  position: relative;
}
.content {
  display: flex;
  align-items: flex-end;
  justify-content: center;
  flex-wrap: wrap;
  background: url($urlImages + "bg6.webp") no-repeat;
  background-size: 100% auto;
  padding-bottom: 0.8rem;
}
.leftbox {
  .cardbox {
    width: 3.35rem;
    height: 5.2rem;
    position: relative;
    > img {
      width: 100%;
      height: 100%;
    }
    span {
      font-size: 0.15rem;
      position: absolute;
      left: 0.2rem;
      top: 0.4rem;
    }
  }
  .workbox {
    width: 3.15rem;
    margin: 0 auto;
    background: #18181c;
    border-radius: 0.04rem;
    border: 1px solid #535151;
    backdrop-filter: blur(0.07rem);
    .titlebtn {
      width: 100%;
      height: 0.6rem;
      background: rgba(129, 129, 151, 0.19);
      backdrop-filter: blur(0.07rem);
      padding: 0 0.1rem;
      display: flex;
      align-items: center;
      justify-content: space-between;
      div {
        display: flex;
        align-items: center;
        font-size: 0.15rem;
        font-weight: 600;
        i {
          font-size: 0.35rem;
          margin-right: 0.1rem;
        }
      }
    }
    .text {
      width: 100%;
      height: 1.15rem;
      font-size: 0.15rem;
      font-weight: 600;
      color: #81838b;
      padding: 0.1rem;
      div {
        width: 100%;
        height: 100%;
        padding: 0 0.1rem;
        overflow-y: auto;
      }
    }
  }
}
.rightbox {
  width: 7.7rem;
  height: 6.8rem;
  background: rgba(129, 129, 151, 0.19);
  border-radius: 0.06rem;
  border: 1px solid #535151;
  backdrop-filter: blur(0.07rem);
  margin-left: 0.2rem;
  > div {
    width: 100%;
    height: 100%;
    background-repeat: no-repeat;
    background-size: auto 100%;
    background-position: right top;
    padding: 0 0.3rem;
    .introbox1 {
      li {
        display: flex;
        align-items: center;
        font-size: 0.12rem;
        font-weight: 600;
        padding: 0.2rem 0;
        &:nth-child(1) {
          font-size: 0.3rem;
          padding: 0.3rem 0;
        }
        i {
          font-size: 0.35rem;
          margin-right: 0.2rem;
        }
        div {
          width: 1.5rem;
          display: flex;
          align-items: center;
        }
      }
    }
    .introbox2 {
      width: 100%;
      height: 2.15rem;
      background: #18181c;
      border-radius: 0.06rem;
      padding: 0.1rem;
      .title {
        width: 100%;
        height: 0.3rem;
        font-size: 0.15rem;
        font-weight: 600;
        padding: 0 0.1rem;
      }
      .text {
        width: 100%;
        height: calc(100% - 0.3rem);
        font-size: 0.15rem;
        font-weight: bold;
        color: #81838b;
        div {
          width: 100%;
          height: 100%;
          padding: 0 0.1rem;
          overflow-y: auto;
        }
      }
    }
  }
}
@media screen and (max-width: 750px) {
  .page {
    width: 100%;
    padding-top: 0.5rem;
  }
  .banner {
    width: 100%;
    height: 0.5rem;
  }
  .content {
    padding-bottom: 0.5rem;
  }
  .leftbox {
    .cardbox {
      width: 2.72rem;
      height: 4.22rem;
      margin: 0 auto;
      margin-bottom: 0.1rem;
      span {
        font-size: 0.12rem;
        left: 0.2rem;
        top: 0.35rem;
      }
    }
    .workbox {
      width: 80%;
      border-radius: 0.02rem;
      margin-bottom: 0.2rem;
      .titlebtn {
        width: 100%;
        height: 0.38rem;
        padding: 0 0.1rem;
        div {
          font-size: 0.12rem;
          font-weight: 600;
          i {
            font-size: 0.15rem;
            margin-right: 0.05rem;
          }
        }
      }
      .text {
        width: 100%;
        height: 0.9rem;
        font-size: 0.12rem;
        font-weight: 600;
        padding: 0.05rem;
        div {
          padding: 0 0.05rem;
        }
      }
    }
  }
  .rightbox {
    width: 80%;
    height: 3.35rem;
    margin-left: 0;
    > div {
      padding: 0 0.1rem;
      .introbox1 {
        li {
          font-size: 0.12rem;
          font-weight: 600;
          padding: 0.08rem 0;
          &:nth-child(1) {
            font-size: 0.15rem;
            padding: 0.1rem 0;
          }
          i {
            font-size: 0.15rem;
            margin-right: 0.1rem;
          }
          div {
            width: 1rem;
          }
        }
      }
      .introbox2 {
        width: 100%;
        height: 1.58rem;
        padding: 0.05rem;
        .title {
          width: 100%;
          height: 0.2rem;
          font-size: 0.15rem;
          font-weight: 600;
          padding: 0 0.05rem;
        }
        .text {
          width: 100%;
          height: calc(100% - 0.2rem);
          font-size: 0.12rem;
          font-weight: bold;
          div {
            padding: 0 0.05rem;
          }
        }
      }
    }
  }
}
</style>
