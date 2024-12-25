<template>
  <div class="container">
    <video ref="videoPlayer" class="video-js"></video>
  </div>
</template>

<script lang="ts" setup>
  import 'video.js/dist/video-js.css';
  import videojs from 'video.js';
  import { onMounted, onBeforeUnmount, ref, effect } from 'vue';

  const videoAddress = ref<string>('');

  const videoPlayer = ref(null);

  effect(() => {
    console.log('effect', videoPlayer.value, videoAddress.value);
    if (videoPlayer.value && videoAddress.value) {
      // 这里添加类型断言，告诉TypeScript videojs期望的第一个参数类型
      videojs(
        videoPlayer.value,
        {
          autoplay: true,
          controls: true,
          sources: [
            {
              src: videoAddress.value,
            },
          ],
        },
        () => {}
      );
    }
  }, [videoPlayer.value,videoAddress.value]);

  const getVideoInfo = () => {
    videoAddress.value = 'https://play.xluuss.com/play/Qe1JAxja/index.m3u8';
  };
  getVideoInfo();
</script>

<style lang="less" scoped>
  .container {
    display: flex;
    height: 100vh;

    .banner {
      width: 550px;
      background: linear-gradient(163.85deg, #1d2129 0%, #00308f 100%);
    }

    .content {
      position: relative;
      display: flex;
      flex: 1;
      align-items: center;
      justify-content: center;
      padding-bottom: 40px;
    }

    .footer {
      position: absolute;
      right: 0;
      bottom: 0;
      width: 100%;
    }
  }

  .logo {
    position: fixed;
    top: 24px;
    left: 22px;
    z-index: 1;
    display: inline-flex;
    align-items: center;

    &-text {
      margin-right: 4px;
      margin-left: 4px;
      color: var(--color-fill-1);
      font-size: 20px;
    }
  }
</style>

<style lang="less" scoped>
  // responsive
  @media (max-width: @screen-lg) {
    .container {
      .banner {
        width: 25%;
      }
    }
  }
</style>
