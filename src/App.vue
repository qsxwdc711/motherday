<template>
  <div class="wrapper">
    <div v-if="currentStep < 0" class="countdown animate__animated animate__fadeInDown">
      {{ Math.abs(currentStep) }}
    </div>

    <div v-else-if="currentStep < messages.length" class="message animate__animated animate__fadeInUp">
      <span class="heart left-heart">❤️</span>
      <span class="text">{{ messages[currentStep] }}</span>
      <span class="heart right-heart">❤️</span>
    </div>

    <div v-else class="message animate__animated animate__zoomIn">
      <span class="heart left-heart">❤️</span>
      <span class="text">我爱您，妈妈！</span>
      <span class="heart right-heart">❤️</span>
    </div>

    <audio :src="musicUrl" autoplay loop ref="audio"></audio>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentStep: -3, // 倒计时从 -3 开始：-3, -2, -1
      messages: [
        "亲爱的妈妈",
        "祝您母亲节快乐！",
        "希望您健健康康",
        "天天开心",
        "辛苦了！老妈！"
      ],
      musicUrl: 'https://cdn.pixabay.com/download/audio/2022/02/15/audio_bf0b51b2f6.mp3?filename=sweet-emotional-piano-3316.mp3'
    };
  },
  mounted() {
    this.$refs.audio.volume = 0.4;
    this.startSequence();
  },
  methods: {
    startSequence() {
      const interval = setInterval(() => {
        this.currentStep++;
        if (this.currentStep > this.messages.length) {
          clearInterval(interval);
        }
      }, 2000); // 每2秒切换一次
    }
  }
};
</script>

<style scoped>
@import 'https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css';

.wrapper {
  background: linear-gradient(to bottom right, #fff5f8, #ffe4e1);
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: "KaiTi", "楷体", serif;
  color: #d81b60;
  text-align: center;
  position: relative;
  overflow: hidden;
}

.countdown {
  font-size: 6rem;
  font-weight: bold;
}

.message {
  font-size: 2.2rem;
  padding: 0 20px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.heart {
  font-size: 2.5rem;
  margin: 0 12px;
  animation: beat 1.5s infinite;
}

.left-heart {
  color: #f06292;
}

.right-heart {
  color: #f06292;
}

@keyframes beat {

  0%,
  100% {
    transform: scale(1);
  }

  50% {
    transform: scale(1.3);
  }
}

.text {
  max-width: 80%;
  word-wrap: break-word;
}
</style>
