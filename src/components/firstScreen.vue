<template>
  <!-- 第一屏 -->
  <div class="screen section1">
    <div class="kv-content">
      <img src="../assets/images/kv.jpg.webp" alt="">
    </div>
  </div>
  <!-- 第二屏 -->
  <div class="screen section2">
    <div class="summary-content">
      <video src="../assets/images/summary.mp4" alt="" class="summary"></video>
      <p class="text1">
        流动山海纹<br>
        光影层叠，山海流淌
      </p>
      <p class="text2">
        东方灵韵，山海情
      </p>
    </div>
  </div>

  <!-- 第三屏 -->
  <div class="screen section3">
    <div class="color-img">
      <img src="../assets/images/color1.png.webp" alt="" class="color1">
      <img src="../assets/images/color2.png.webp" alt="" class="color2">
      <img src="../assets/images/color3.png.webp" alt="" class="color3">
      <img src="../assets/images/color4.png.webp" alt="" class="color4">
    </div>
  </div>
</template>

<script setup>
import { onMounted } from "vue";
// typical import
import gsap from "gsap";
// get other plugins:
import ScrollTrigger from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);

onMounted(() => {
  // 第一屏
  firstScreen()
  // 第二屏
  secondScreen()
  // 第三屏
  thirdlyScreen()

})




// 第一屏
const firstScreen = () => {
  ScrollTrigger.create({
    trigger: '.section1',
    start: 'top top',
    end: '+=1000',
    scrub: true,
    animation:
      // gsap.fromTo('.kv-content', { scale: 1 }, { scale: 0.5 })
      gsap.timeline().fromTo('.kv-content', { scale: 1 }, { scale: 0.5 })
        // .fromTo('.summary-content', { scale: .5 }, { scale: 1 }, '<')
        .fromTo('.summary-content', {
          width: '50%', height: '50%'
        }, { width: '100%', height: '100%' }, '<')
  })
}

// 第二屏
const secondScreen = () => {
  ScrollTrigger.create({
    trigger: '.section2',
    start: 'top top',
    end: '+=5000',
    scrub: true,
    // 固定屏幕
    pin: true,
    // 滚动条滚动，视频播放
    // onUpdate ScrollTrigger 的进度（意味着滚动位置更改）时会调用此函数
    onUpdate(self) {
      const summary = document.querySelector('.summary')
      try {
        // 视频的播放进度随着滚动条变化
        // self.progress 整体滚动进度 0-1
        // summary.duration 视频总时长
        // summary.currentTime 视频播放进度
        summary.currentTime = self.progress * summary.duration
      } catch (error) {
        console.log(error);
      }
    },
    animation:
      gsap.timeline()
        .to('.text1', { top: '20rem', opacity: 1 },)
        .to('.text1', { top: 0, opacity: 0 })
        .to('.text2', { top: '27rem', opacity: 1 },)
        .to('.text2', { top: '20rem', opacity: 0 })
  })
}

// 第三屏
const thirdlyScreen = () => {
  ScrollTrigger.create({
    trigger: '.section3',
    start: 'top top',
    end: '+=1000',
    pin: true,
    markers: true, // 标记位置
  })

  ScrollTrigger.create({
    trigger: '.color-img',
    start: 'top-=500 top',
    end: '+=3000',
    scrub: true,
    animation: gsap.timeline()
      .fromTo('.color1', { 'margin-left': '80em', opacity: 0 }, { 'margin-left': 0, opacity: 1 }, '<')
      .fromTo('.color2', { 'margin-left': '100em', scale: 1.3 }, { 'margin-left': 0, scale: 1 }, '<')
      .fromTo('.color3', { 'margin-left': '110em', scale: 1.6 }, { 'margin-left': 0, scale: 1 }, '<')
      .fromTo('.color4', { 'margin-left': '120em', scale: 1.9 }, { 'margin-left': 0, scale: 1 }, '<')
      .fromTo('.color1', { 'margin-left': '0', opacity: 1 }, { 'margin-left': '-120em', opacity: 1 }, '>')
      .fromTo('.color2', { 'margin-left': '0', scale: 1 }, { 'margin-left': '-110em', scale: 1.3 }, '<')
      .fromTo('.color3', { 'margin-left': '0', scale: 1 }, { 'margin-left': '-100em', scale: 1.6 }, '<')
      .fromTo('.color4', { 'margin-left': '0', scale: 1 }, { 'margin-left': '-90em', scale: 1.9 }, '<')
  })
}

</script>

<style scoped>
/* 第一屏 */
.screen {
  position: relative;
  width: 100%;
  height: 100vh;
  overflow: hidden;
}

.kv-content {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100%;
  height: 100vh;
}

.kv-content img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

/* 第二屏 */
.summary-content {
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 100%;
  height: 100vh;
}

.summary-content video {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.summary-content .text1 {
  position: absolute;
  top: 60rem;
  left: 10rem;
  opacity: 0;
  font-size: 4rem;
  color: #fff;
  z-index: 999;
}

.summary-content .text2 {
  position: absolute;
  top: 30rem;
  left: 2rem;
  opacity: 0;
  font-size: 5rem;
  color: #fff;
}

/* 第三屏 */
.section3 {
  height: 200vh;
}

.color-img {
  width: 30em;
  position: absolute;
  top: 10em;
  left: 40em;
}

.color1 {
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  margin-left: 90em;
}

.color2 {
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  margin-left: 100em;
  scale: 1.1;
}

.color3 {
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  margin-left: 110em;
  scale: 1.2;
}

.color4 {
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  margin-left: 120em;
  scale: 1.3;
}
</style>
