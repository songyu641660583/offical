<script setup lang="ts">
import 'animate.css';
import { NDropdown, NSpace, NIcon } from 'naive-ui'
import { ref, onMounted } from 'vue'
import { EarthOutline, ChevronDownSharp } from '@vicons/ionicons5'
import languageData from './utils/language'


const languageOptions = [
  {
    label: '中文',
    key: 'chinese'
  },
  {
    label: 'English',
    key: 'english'
  }
]

type languateType = 'chinese' | 'english'

const languageValue = ref<string>(localStorage.getItem('languageValue') || 'chinese')

const languageDic = ref<any>(languageData[languageValue.value as languateType])

const animationRef = ref<Element[]>([])

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('customFadeInUp');
          observer.unobserve(entry.target);
        }
      });
    },
    {
      threshold: 0.2, 
    }
  );
  animationRef.value.forEach((item) => {
    observer.observe(item);
  });
});
const handleContentItemRef = (el: any) => {
  if (el) {
    animationRef.value.push(el);
  }
};


const handleSelect = (key: string) => {
  languageValue.value = key
  languageDic.value = languageData[languageValue.value as languateType]
  localStorage.setItem('languageValue', key)
}

function getLanguageText() {
  return languageOptions.find((item) => item.key === languageValue.value)?.label
}

const numberValue = ref('11')

function numberChange(value = '11') {
  if (value === '11') {
    numberValue.value = '01'
  }
  if (value === '10') {
    numberValue.value = '11'
  }
  if (value === '01') {
    numberValue.value = '00'
  }
  if (value === '00') {
    numberValue.value = '10'
  }
}
setInterval(() => {
  numberChange(numberValue.value)
}, 200)
</script>

<template>
  <div class="home-page">
    <!-- 头部导航栏 -->
    <div class="header">
      <div class="header-in">
        <div class="header-left">
          <div class="header-logo"><img src="@/assets/logo.png" alt=""></div>
          <span>Silverstream</span>
        </div>
        <div class="header-right">
          <n-space>
            <n-dropdown trigger="click" :options="languageOptions" @select="handleSelect">
              <div class="language-drop">
                <n-icon size="22">
                  <EarthOutline />
                </n-icon>
                <span class="text">{{ getLanguageText() }}</span>
                <n-icon size="18">
                  <ChevronDownSharp />
                </n-icon>
              </div>
            </n-dropdown>
          </n-space>
        </div>
      </div>
    </div>
    <!--AI驱动的交易策略开发  -->
    <div class="ai-power">
      <div class="ai-power-title">
        <span class="title">{{ languageDic.aiPower.title }}</span>
        <div class="star">
          <img class="start-1" src="@/assets/ai-power-star.png" alt="">
          <img class="start-2" src="@/assets/ai-power-star2.png" alt="">
        </div>
        <span class="title" v-html="languageDic.aiPower.title2"></span>
      </div>
      <div class="ai-power-content" v-html="languageDic.aiPower.content"></div>
      <div class="ai-power-btn">{{languageDic.aiPower.btnText}}</div>
      <div class="ai-power-line">
        <div class="ai-power-item first">
          <div class="move-block">
            <div class="block gray"></div>
            <div class="circle"></div>
          </div>
        </div>
        <div class="ai-power-item second">
          <div class="move-block">
            <div class="block green"></div>
            <div class="circle"></div>
          </div>
        </div>
        <div class="ai-power-item third">
          <div class="move-block">
            <div class="circle"></div>
            <div class="block black"></div>
          </div>
        </div>
        <div class="ai-power-item fourth">
          <div class="move-block">
            <div class="circle"></div>
            <div class="block green"></div>
          </div>
        </div>
        <div class="ai-power-item fiveth">
          <div class="move-block">
            <div class="block gray"></div>
            <div class="circle"></div>
          </div>
        </div>
      </div>
     
      <div class="ai-card1">
        <div></div>
      </div>
      <div class="ai-card2">
        <div><span>{{ numberValue }}</span></div>
      </div>
      <div class="ai-card3">
        <div>
          <span></span>
          <span></span>
          <span></span>
          <span></span>
        </div>
      </div>
      <div class="ai-card4">
        <div>

        </div>
      </div>
    </div>
    <!-- 关键能力 -->
    <div class="key-features">
      <div class="key-features-in">
        <div class="key-features-title animationElement" :ref="(el) => handleContentItemRef(el)">{{ languageDic.keyFeatures.title }}</div>
        <div class="key-features-content animationElement" :ref="(el) => handleContentItemRef(el)" v-html="languageDic.keyFeatures.content"></div>
        <div class="kf-card1 animationElement" :ref="(el) => handleContentItemRef(el)">
          <div class="kf-card1-left card-box">
            <div class="kf-card1-left-title title">{{ languageDic.keyFeatures.card1Title }}</div>
            <div class="kf-card1-left-content content">{{ languageDic.keyFeatures.card1Content }}</div>
            <div class="kf-card1-left-img">
              <img src="@/assets/kf-card1-bg.png" alt="">
            </div>
          </div>
          <div class="kf-card1-right card-box">
            <div class="kf-card1-right-img">
              <img src="@/assets/kf-card2-bg.png" alt="">
            </div>
            <div class="title">{{ languageDic.keyFeatures.card2Title }}</div>
            <div class="content" v-html="languageDic.keyFeatures.card2Content"></div>
          </div>

        </div>
        <div class="kf-card2  animationElement" :ref="(el) => handleContentItemRef(el)">
          <div class="kf-card2-left card-box">
            <div class="kf-card2-left-in">
              <div class="title">{{ languageDic.keyFeatures.card3Title }}</div>
              <div class="content" v-html="languageDic.keyFeatures.card3Content"></div>
            </div>
          </div>
          <div class="kf-card2-right card-box">
            <div class="kf-card2-right-direc">
              <div class="title">{{ languageDic.keyFeatures.card4Title }}</div>
              <div class="content" v-html="languageDic.keyFeatures.card4Content"></div>
            </div>
            <div class="kf-card2-right-img"> <img src="@/assets/kf-card4-bg.png" alt=""></div>
          </div>
        </div>
        <div class="kf-footer animationElement" :ref="(el) => handleContentItemRef(el)">
          <div class="kf-footer-tips" v-html="languageDic.keyFeatures.tips"></div>
          <div class="kf-footer-type">
            <span>Python</span>
            <span>Pine Script</span>
            <span>MQL</span>
          </div>
        </div>
      </div>
    </div>

    <div class="prd-module">
      <div class="prd-module-in">
        <!-- 算法开发助手 -->
        <div class="prd-card1 animationElement" :ref="(el) => handleContentItemRef(el)">
          <div class="prd-title">{{ languageDic.prd.card1Title }}</div>
          <div class="prd-content" v-html="languageDic.prd.card1Content"></div>
          <div class="prd-img">
            <img src="@/assets/prd-card1-bg.png" alt="">
          </div>
        </div>
        <div class="hr"></div>
        <div class="prd-flex animationElement" :ref="(el) => handleContentItemRef(el)">
          <div class="prd-card2">
            <div class="prd-title">{{ languageDic.prd.card2Title }}</div>
            <div class="prd-content" v-html="languageDic.prd.card2Content"></div>
            <div class="prd-img">
              <img src="@/assets/prd-card2-bg.png" alt="">
            </div>
          </div>
          <div class="prd-card3">
            <div class="line"></div>
            <div class="prd-title">{{ languageDic.prd.card3Title }}</div>
            <div class="prd-content" v-html="languageDic.prd.card3Content"></div>
            <div class="prd-img">
              <img src="@/assets/prd-card3-bg.png" alt="">
            </div>
          </div>
        </div>
        <div class="hr"></div>
        <div class="prd-flex animationElement" :ref="(el) => handleContentItemRef(el)">
          <!-- 模块化开发 -->
          <div class="prd-card4">
            <div class="prd-title">{{ languageDic.prd.card4Title }}</div>
            <div class="prd-content" v-html="languageDic.prd.card4Content"></div>
            <div class="prd-img">
              <img src="@/assets/prd-card4-bg.png" alt="">
            </div>
          </div>
          <!-- 模块化交易框架 -->
          <div class="prd-card5">
            <div class="line"></div>
            <div class="prd-title">{{ languageDic.prd.card5Title }}</div>
            <div class="prd-content" v-html="languageDic.prd.card5Content"></div>
            <div class="prd-img">
              <img src="@/assets/prd-card5-bg.png" alt="">
            </div>
          </div>
        </div>
        <div class="hr"></div>
        <div class="prd-flex animationElement" :ref="(el) => handleContentItemRef(el)">
          <!-- 回测平台 -->
          <div class="prd-card6">
            <div class="prd-title">{{ languageDic.prd.card6Title }}</div>
            <div class="prd-content" v-html="languageDic.prd.card6Content"></div>
            <div class="prd-img">
              <img src="@/assets/prd-card6-bg.png" alt="">
            </div>
          </div>
          <!-- AI交易验证 -->
          <div class="prd-card7">
            <div class="line grident"></div>
            <div class="prd-title">{{ languageDic.prd.card7Title }}</div>
            <div class="prd-content" v-html="languageDic.prd.card7Content"></div>
            <div class="prd-img">
              <img src="@/assets/prd-card7-bg.png" alt="">
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- 视频资源模块  为您的交易之旅增添光彩-->
    <div class="video-module animationElement" :ref="(el) => handleContentItemRef(el)">
      <div class="video-mark">
        <div class="video-module-title">{{ languageDic.video.title }}</div>
        <div class="video-module-content" v-html="languageDic.video.content1"></div>
        <div class="video-module-content" v-html="languageDic.video.content2" style="margin-top: 30px"></div>
      </div>
      <video autoplay muted loop>
        <source src="@/assets/video.mp4" type="video/mp4">
      </video>
    </div>
    <div class="learn-module">
      <!-- 快速学习的教育内容 -->
      <div class="learn-module-in">
        <div class="learn-tips animationElement" :ref="(el) => handleContentItemRef(el)">{{ languageDic.learn.tips }}</div>
        <div class="learn-title animationElement" v-html="languageDic.learn.title" :ref="(el) => handleContentItemRef(el)"></div>
        <div class="learn-content animationElement" :ref="(el) => handleContentItemRef(el)">{{ languageDic.learn.content }}</div>
        <div class="learn-main">
          <!-- 交易算法开发指南 -->
          <div class="learn-main-item animationElement" :ref="(el) => handleContentItemRef(el)">
            <div class="learn-main-item-title" v-html="languageDic.learn.card1Title"></div>
            <div class="learn-main-item-content" v-html="languageDic.learn.card1Content"></div>
            <div class="learn-main-item-img">
              <img src="@/assets/learn-icon1.png" alt="">
            </div>
          </div>
          <!-- 模块化交易策略教程-->
          <div class="learn-main-item animationElement" :ref="(el) => handleContentItemRef(el)">
            <div class="learn-main-item-title" v-html="languageDic.learn.card2Title"></div>
            <div class="learn-main-item-content" v-html="languageDic.learn.card2Content"></div>
            <div class="learn-main-item-img">
              <img src="@/assets/learn-icon2.png" alt="">
            </div>
          </div>
          <!-- 人工智能在交易策略开发中的应用 -->
          <div class="learn-main-item animationElement" :ref="(el) => handleContentItemRef(el)">
            <div class="learn-main-item-title" v-html="languageDic.learn.card3Title"></div>
            <div class="learn-main-item-content" v-html="languageDic.learn.card3Content"></div>
            <div class="learn-main-item-img">
              <img src="@/assets/learn-icon3.png" alt="">
            </div>
          </div>
          <!-- 交易策略验证的最佳实践 -->
          <div class="learn-main-item animationElement" :ref="(el) => handleContentItemRef(el)">
            <div class="learn-main-item-title" v-html="languageDic.learn.card4Title"></div>
            <div class="learn-main-item-content" v-html="languageDic.learn.card4Content"></div>
            <div class="learn-main-item-img">
              <img src="@/assets/learn-icon4.png" alt="">
            </div>
          </div>
          <!-- 市场状态分析的理解 -->
          <div class="learn-main-item animationElement" :ref="(el) => handleContentItemRef(el)">
            <div class="learn-main-item-title" v-html="languageDic.learn.card5Title"></div>
            <div class="learn-main-item-content" v-html="languageDic.learn.card5Content"></div>
            <div class="learn-main-item-img">
              <img src="@/assets/learn-icon5.png" alt="">
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="design-module">
<!-- 以用户体验为中心的设计 -->
      <div class="design-module-in">
        <div class="design-tips animationElement"  :ref="(el) => handleContentItemRef(el)">{{ languageDic.design.tips }}</div>
        <div class="design-title animationElement" v-html="languageDic.design.title"  :ref="(el) => handleContentItemRef(el)"></div>
        <div class="design-content animationElement"  :ref="(el) => handleContentItemRef(el)">{{ languageDic.design.content }}</div>
        <!-- 清晰的导航结构 -->
        <div class="design-item one animationElement" :ref="(el) => handleContentItemRef(el)">
          <div class="design-item-img">
            <img src="@/assets/design-icon1.png" alt="">
          </div>
          <div class="design-item-title" v-html="languageDic.design.card1Title"></div>
          <div class="design-item-content" v-html="languageDic.design.card1Content"></div>
        </div>
        <!-- 易于遵循的教 -->
        <div class="design-item two animationElement" :ref="(el) => handleContentItemRef(el)">
          <div class="design-item-img">
            <img src="@/assets/design-icon2.png" alt="">
          </div>
          <div class="design-item-desc">
            <div class="design-item-title" v-html="languageDic.design.card2Title"></div>
            <div class="design-item-content" v-html="languageDic.design.card2Content"></div>
          </div>
        </div>
        <!-- 快速入门指南-->
        <div class="design-item three animationElement" :ref="(el) => handleContentItemRef(el)">
          <div class="design-item-img">
            <img src="@/assets/design-icon3.png" alt="">
          </div>
          <div class="design-item-desc">
            <div class="design-item-title" v-html="languageDic.design.card3Title"></div>
            <div class="design-item-content" v-html="languageDic.design.card3Content"></div>
          </div>
        </div>
        <!-- 互动演示部分 -->
        <div class="design-item four animationElement" :ref="(el) => handleContentItemRef(el)" style="width: 420px">
          <div class="design-item-img">
            <img src="@/assets/design-icon4.png" alt="">
          </div>
          <div class="design-item-desc">
            <div class="design-item-title" v-html="languageDic.design.card4Title"></div>
            <div class="design-item-content" v-html="languageDic.design.card4Content"></div>
          </div>
        </div>
      </div>
    </div>
    <div class="marketing-module">
      <!-- 内容营销与教育推广 -->
      <div class="marketing-module-in animationElement" :ref="(el) => handleContentItemRef(el)">
        <div class="marketing-tips">{{ languageDic.marketing.tips }}</div>
        <div class="marketing-title" v-html="languageDic.marketing.title"></div>
        <div class="marketing-content">{{ languageDic.marketing.content }}</div>
        <!-- 博客文章 -->
        <div class="marketing-item">
          <div class="marketing-item-title" v-html="languageDic.marketing.title1"></div>
          <div class="marketing-item-content" v-html="languageDic.marketing.content1"></div>
        </div>
        <!-- 案例研究 -->
        <div class="marketing-item">
          <div class="marketing-item-title" v-html="languageDic.marketing.title2"></div>
          <div class="marketing-item-content" v-html="languageDic.marketing.content2"></div>
        </div>
        <!-- 教程视频 -->
        <div class="marketing-item">
          <div class="marketing-item-title" v-html="languageDic.marketing.title3"></div>
          <div class="marketing-item-content" v-html="languageDic.marketing.content3"></div>
        </div>
        <!-- 全面的文档-->
        <div class="marketing-item">
          <div class="marketing-item-title" v-html="languageDic.marketing.title4"></div>
          <div class="marketing-item-content" v-html="languageDic.marketing.content4"></div>
        </div>
        <!-- 成功故事 -->
        <div class="marketing-item">
          <div class="marketing-item-title" v-html="languageDic.marketing.title5"></div>
          <div class="marketing-item-content" v-html="languageDic.marketing.content5"></div>
        </div>
        <!-- 右侧公转模块 -->
        <div class="marketing-bg">
          <img class="marketing-bg-icon3" src="@/assets/marketing-icon3.png" alt="">

          <div class="mark">
            <img class="mark-icon1" src="@/assets/marketing-icon1.png" alt="">
            <img class="mark-icon4" src="@/assets/marketing-icon4.png" alt="">
            <img class="mark-icon5" src="@/assets/marketing-icon5.png" alt="">
          </div>
          <div class="mark mark2">

            <img class="mark2-icon2" src="@/assets/marketing-icon2.png" alt="">

          </div>

        </div>
      </div>
    </div>
    <!-- 底部菜单栏 -->
    <div class="footer">
      <div class="footer-in">
        <div class="f-name">
          Silverstream
        </div>
        <div class="f-classify">
          <div class="f-classify-content">

            <div class="f-column" v-for="item in languageDic.footer" :key="item.key">
              <div class="f-column-name">{{ item.key }}</div>
              <div class="f-column-item" v-for="(child) in item.data" :key="child.name">{{ child.name }}</div>
            </div>
          </div>
          <div class="f-classify-btn">SUBSCRIBE</div>
        </div>
        <div class="f-copyright">
          Copyright © 2025 Silverstream 保留所有权
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
$contentWidth: 1280px;
@use './css/aiPower';
@use './css/keyFeature';
@use './css/video';
@use './css/prd';
@use './css/learn';
@use './css/design';
@use './css/marketing';

.home-page {
  width: 100vw;
  height: 100vh;
  overflow-y: scroll;

  &::-webkit-scrollbar {
    width: 0;
    height: 0;
  }

  .header {
    position: sticky;
    top: 0;
    z-index: 1000;
    width: 100%;
    height: 64px;
    background-color: #f8f8f8;
    border-bottom: 1px solid #e9e9e9;

    .header-in {
      display: flex;
      justify-content: space-between;
      align-items: center;
      height: 64px;
      width: $contentWidth;
      margin: 0 auto;

      .header-left {
        display: flex;
        align-items: center;
        color: #000000;
        font-size: 20px;
        font-weight: 600;

        .header-logo {
          margin-right: 5px;
          display: flex;
          align-items: center;
          img {
            width: 30px;
          }
        }
      }

      .language-drop {
        display: flex;
        align-items: center;
        color: #000;
        cursor: pointer;

        .text {
          margin: 0 10px 0 5px;
          font-size: 14px;
          font-weight: 500;
        }
      }
    }
  }



  .footer {
    height: 609px;

    background-color: #000;
    box-sizing: border-box;
    color: #fff;
    overflow: hidden;

    .footer-in {
      margin: 0 auto;
      padding-top: 120px;
      width: $contentWidth;
    }

    .f-name {
      font-size: 48px;
      font-weight: 600;

    }

    .f-classify {
      display: flex;
      justify-content: space-between;

      &-content {
        display: flex;
        justify-content: space-between;
        margin-top: 44px;
        width: 849px;

        .f-column {
          &-name {
            margin-bottom: 20px;
            font-size: 18px;
            font-weight: 700;
          }

          &-item {
            margin-bottom: 8px;
            line-height: 26px;
            font-size: 16px;
            font-weight: 400;
            color: #bcbed2;
          }
        }
      }

      &-btn {
        display: flex;
        align-items: center;
        justify-content: center;
        margin-top: 44px;
        width: 151px;
        height: 52px;

        border-radius: 4px;
        background-color: #fff;
        color: #000;
        font-size: 16px;
        font-weight: 700;

      }
    }

    .f-copyright {
      margin-top: 33px;
      padding-top: 32px;
      border-top: 1px solid #bcbed2;
      font-size: 12px;
      font-weight: 400;
      color: #bcbed2;
    }

  }
}

.animationElement {
  opacity: 0;
  &.customFadeInUp{
    opacity: 1;
    animation: customFadeInUp 1s ease;
  }
}

@keyframes customFadeInUp {
  from {
    opacity: 0;
    // 调整渐入的距离 40px是要修改的值，数值越大距离越大;
    transform: translateY(40px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}


</style>
