<template>
  <div class="work-container onedoctor">
    <!-- 공통 상단 영역 시작 -->
    <WorkContentCommon />

    <div class="works-content">
      <img src="/works/onedoctor/image_pc_01.png" class="only-pc" />
      <img src="/works/onedoctor/image_mobile_01.png" class="only-mobile" />
    </div>

    <section class="works-content section01">
      <div class="section-inner">
        <div class="section-texts">
          <img
            class="section-icon"
            src="/works/onedoctor/section01_icon.png"
            alt=""
          />
          <p class="section-title">채팅 UI를 활용한 친근감 형성</p>
          <p class="section-description">
            사용자가 건강기록을 입력하면 의료 전문가와 직접 상담하는듯한 답변이
            제공됩니다.<br />
            버튼을 선택함으로써 사용자가 번거로운 타이핑 작업을 하지 않아도
            자연스러운 플로우가 진행됩니다.
          </p>
        </div>
        <div class="section-images">
          <img src="/works/onedoctor/section01_image01.png" />
          <img src="/works/onedoctor/section01_image02.png" />
          <img src="/works/onedoctor/section01_image03.png" />
          <img src="/works/onedoctor/section01_image04.png" />
        </div>
      </div>
    </section>
    <section class="works-content section02">
      <div class="section-inner">
        <div class="section-texts">
          <img
            class="section-icon"
            src="/works/onedoctor/section02_icon.png"
            alt=""
          />
          <p class="section-title">등록된 디바이스와의 자동 호환</p>
          <p class="section-description">
            사용자가 현재 사용하고 있는 혈압계 · 혈당계를 원닥터 앱과 동기화시켜
            직접 입력할 필요 없이 블루투스를 이용한 자동 전송 기능을 활용하여
            누구나 쉽게 건강기록 관리가 가능합니다.
          </p>
        </div>
        <div class="section-images">
          <img src="/works/onedoctor/section02_image01.png" />
          <img src="/works/onedoctor/section02_image02.png" />
        </div>
      </div>
    </section>
    <section class="works-content section03">
      <div class="section-inner">
        <div class="section-texts">
          <img
            class="section-icon"
            src="/works/onedoctor/section03_icon.png"
            alt=""
          />
          <p class="section-title">친절하고 따뜻한 UX라이팅</p>
          <p class="section-description">
            의사선생님과 직접 소통하는듯이 친절하고 따뜻한 말투의 통일된 UX
            라이팅을 용하여 사용자에게 친근감있게 다가갑니다.
          </p>
        </div>
        <div class="section-images">
          <div class="section-circles">
            <div></div>
            <div></div>
            <div></div>
          </div>
          <img src="/works/onedoctor/section03_image01.png" />
          <img src="/works/onedoctor/section03_image02.png" />
          <img src="/works/onedoctor/section03_image03.png" />
          <img src="/works/onedoctor/section03_image04.png" class="only-pc" />
          <img src="/works/onedoctor/section03_image05.png" />
        </div>
      </div>
    </section>
    <!-- 공통 상단 영역 종료 -->
  </div>
</template>
<script setup>
import { onMounted, defineProps } from "vue";
import WorkContentCommon from "@/views/WorkContentCommon.vue";
</script>
<style lang="scss">
@import "../assets/scss/response.scss";
// 공통
.onedoctor .section01,
.onedoctor .section02,
.onedoctor .section03 {
  background-color: #fff;
}
.onedoctor {
  .section-inner {
    display: flex;
    align-items: center;
    gap: 196px;

    max-width: 1096px;
    margin: 0 auto;
    padding: 120px 0;

    position: relative;
  }
  .section-icon {
    // 공통에서 16px로 잡힘;
    border-radius: 0 !important;
  }
  .section-title {
    font-size: 50px;
    line-height: 60px;
    font-weight: bold;
    color: #000;
    word-break: keep-all;

    opacity: 0;
    transform: scale(1) translateY(200px);
    transition: all ease-out 0.8s;
    transition-delay: var(--delayImg);
  }
  .section-description {
    font-size: 16px;
    line-height: 24px;
    color: #000;

    opacity: 0;
    transform: scale(1) translateY(200px);
    transition: all ease-out 0.8s;
    transition-delay: var(--delayImg);
  }

  .section01 {
    border-radius: 16px 16px 0 0 !important;
    .section-inner {
      .section-texts {
        display: flex;
        flex-direction: column;
        width: 100%;
        max-width: 420px;
        gap: 24px;

        img {
          width: 54px;
        }
      }
      .section-images {
        display: flex;
        justify-content: center;
        max-width: 480px;
        position: relative;

        img:nth-of-type(1) {
          max-width: 384px;
        }
        img:nth-of-type(2) {
          max-width: 132px;
          position: absolute;
          bottom: 188px;
          right: 90px;
        }
        img:nth-of-type(3) {
          max-width: 280px;
          position: absolute;
          bottom: 28px;
          left: 0;
        }
        img:nth-of-type(4) {
          max-width: 280px;
          position: absolute;
          bottom: -36px;
          left: 0;
        }
      }
    }
  }

  .section02 {
    margin-top: 0 !important;
    border-radius: 0 !important;
    .section-inner {
      flex-direction: row-reverse;

      .section-texts {
        display: flex;
        flex-direction: column;
        max-width: 420px;
        gap: 24px;

        img {
          width: 39px;
        }
      }
      .section-images {
        display: flex;
        justify-content: center;
        max-width: 480px;
        position: relative;

        img:nth-of-type(1) {
          max-width: 360px;
          text-align: center;
        }
        img:nth-of-type(2) {
          position: absolute;
          left: 0;
          right: 0;
          bottom: 24px;
        }
      }
    }
  }

  .section03 {
    margin-top: 0 !important;
    padding-bottom: 120px;
    border-radius: 0 0 16px 16px !important;
    .section-inner {
      align-items: flex-start;
      max-width: 1200px;
      gap: 0;

      .section-texts {
        display: flex;
        flex-direction: column;
        min-width: 420px;
        gap: 24px;

        img {
          width: 50px;
        }
      }
      .section-images {
        display: flex;
        justify-content: center;
        min-width: 938px;
        height: 938px;
        position: relative;
        z-index: 1;

        // 그림자 숨기고 다시 export 해야 함.

        img {
          width: auto;
          height: 113.7px;
        }

        img:nth-of-type(1) {
          max-width: 360px;
          height: fit-content;
          margin-top: 103px;
        }
        img:nth-of-type(2) {
          position: absolute;
          top: 228px;
          right: 50.45px;
        }
        img:nth-of-type(3) {
          position: absolute;
          top: 467px;
          left: -64px;
        }
        img:nth-of-type(4) {
          position: absolute;
          bottom: 77.35px;
          right: 58px;
        }
        img:nth-of-type(5) {
          position: absolute;
          bottom: -14px;
          left: 39px;
        }
      }

      .section-circles {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100%;
        height: 100%;
        position: absolute;
        right: 0;
        top: 0;

        div {
          border-radius: 50%;
          box-sizing: border-box;
          position: absolute;

          transition: all 0.4s ease;
          transform: scale(0);
        }
        div:nth-of-type(1) {
          // 534px
          width: 56%;
          padding-top: 56%;
          background-color: rgba(34, 185, 159, 0.07);
        }
        div:nth-of-type(2) {
          // 734px
          width: 78%;
          padding-top: 78%;
          background-color: rgba(34, 185, 159, 0.07);
        }
        div:nth-of-type(3) {
          width: 100%;
          padding-top: 100%;
          border: 1px solid rgba(34, 185, 159, 0.3);
        }
      }
    }
  }

  .works-content.show {
    .section-texts {
      .section-icon {
        opacity: 1;
        transform: translateY(0);
        --delayImg: 0.25s;
      }
      .section-title {
        opacity: 1;
        transform: translateY(0);
        --delayImg: 0.5s;
      }
      .section-description {
        opacity: 1;
        transform: translateY(0);
        --delayImg: 0.75s;
      }
    }
    .section-images {
      img {
        opacity: 1;
        transform: translateY(0);
        --delayImg: 1.25s;
      }
      img:nth-of-type(1) {
      }
      img:nth-of-type(2) {
        --delayImg: 1.5s;
      }
      img:nth-of-type(3) {
        --delayImg: 1.75s;
      }
      img:nth-of-type(4) {
        --delayImg: 2s;
      }
    }
    &.section03 {
      .section-circles {
        div {
          transform: scale(1);
        }
        div:nth-of-type(1) {
          transition-delay: 1.5s;
        }
        div:nth-of-type(2) {
          transition-delay: 2s;
        }
        div:nth-of-type(3) {
          transition-delay: 2.5s;
        }
      }
      .section-images {
        img:nth-of-type(1) {
        }
        img:nth-of-type(2) {
          --delayImg: 2.75s;
        }
        img:nth-of-type(3) {
          --delayImg: 3s;
        }
        img:nth-of-type(4) {
          --delayImg: 3.25s;
        }
        img:nth-of-type(5) {
          --delayImg: 3.5s;
        }
      }
    }
  }

  @include for-size-max("xlarge") {
    .section-title {
      font-size: 24px;
      line-height: 30px;
    }
    .section-description {
      font-size: 14px;
      line-height: 18px;
    }
    .section-inner {
      flex-direction: column !important;
      gap: 32px;
    }
    .section-texts {
      padding-inline: 32px;
    }

    .section01 {
      .section-inner {
        .section-images {
          margin: 0 20px;
        }
      }
    }

    .section02 {
      .section-inner {
        .section-images {
          margin: 0 20px;

          img:nth-of-type(2) {
            width: calc(100% + 10px);
            max-width: calc(100% + 10px);
            left: -7px;
            right: -5px;
            bottom: 12px;
          }
        }
      }
    }

    .section03 .section-inner {
      align-items: center;
      gap: 32px;
      .section-texts {
        max-width: 420px;
        min-width: auto;
      }
      .section-images {
        margin: 0 20px;

        img {
          // TODO 고정된 height가 아니라 각각 width를 줘야 함..???
          height: 80px;
        }

        .section-circles {
        }

        img:nth-of-type(1) {
          width: 100%;
        }

        img:nth-of-type(2) {
          top: 40%;
          right: 5%;
        }

        img:nth-of-type(2) {
          top: 45%;
          right: -4%;
        }
        img:nth-of-type(3) {
          top: 50%;
          left: -5%;
        }
        img:nth-of-type(4) {
          bottom: 10%;
          right: -5%;
        }
        img:nth-of-type(5) {
          bottom: 5%;
          left: -2%;
        }
      }
    }
  }

  @include for-size-max("extra-small") {
    .section-inner {
      padding: 60px 0;
      // max-width: 200px !important;
    }
    .section03 {
      padding: 0;
      .section-inner {
        // align-items: center;
        // gap: 32px;
        // .section-texts {
        //   max-width: 420px;
        //   min-width: auto;
        // }
        .section-images {
          // margin: 0 20px;

          img {
            // TODO 고정된 height가 아니라 각각 width를 줘야 함..???
            height: 22.222dvw;
          }
          height: 108.333vw;

          img:nth-of-type(1) {
            margin-top: 10.556vw;
            width: 45.556svw;
            height: auto;
          }
          img:nth-of-type(2) {
            top: 45.167vw;
            right: auto;
            margin-left: 52.556vw;
          }
          img:nth-of-type(3) {
            top: 0;
            left: auto;
            margin-right: 43.611vw;
          }
          img:nth-of-type(5) {
            bottom: 0;
            left: auto;
            margin-right: 46.389vw;
          }
        }
        .section-circles {
          div:nth-of-type(1) {
            width: 74.444dvw;
            height: 74.444dvw;
            padding-top: 0;
          }
          div:nth-of-type(2) {
            // 734px
            width: 100vw;
            height: 100vw;
            padding-top: 0;
          }
          div:nth-of-type(3) {
            display: none;
          }
        }
      }
    }
  }
}
</style>
