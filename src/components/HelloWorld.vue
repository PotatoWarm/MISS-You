<template>
  <div class="comfort-container">
    <div class="header">
      <h2>{{ currentMood ? '让我来哄哄你～' : '亲爱的，心情不好吗？' }}</h2>
    </div>

    <div v-if="!currentMood" class="mood-selection">
      <button 
        v-for="(mood, index) in moods" 
        :key="index"
        @click="selectMood(mood)"
        class="mood-btn">
        {{ mood.name }}
      </button>
    </div>

    <div v-else class="comfort-content">
      <div class="message-box">
        {{ currentMessage }}
      </div>
      
      <div class="action-buttons">
        <button @click="showNextMessage" class="action-btn">
          换一个
        </button>
        <button @click="resetMood" class="action-btn">
          重新选择心情
        </button>
      </div>

      <div class="love-meter">
        <div class="hearts">
          <span v-for="n in loveCount" :key="n" class="heart">❤️</span>
        </div>
        <button @click="increaseLove" class="love-btn">
          点击增加爱心
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentMood: null,
      currentMessageIndex: 0,
      loveCount: 0,
      moods: [
        {
          name: '工作累了',
          messages: [
            '辛苦啦！要不要我给你捶捶背？',
            '今天工作这么拼，真让人心疼～',
            '累了就休息一下，我陪你聊天',
            '要不要一起出去散散步？换换心情～',
            '你已经做得很好了，放松一下吧'
          ]
        },
        {
          name: '心情不好',
          messages: [
            '抱抱～不开心的事情说出来会好一点',
            '有我在呢，别担心～',
            '要不要听听你最喜欢的音乐？',
            '我永远支持你、相信你',
            '不开心的时候，想想我好不好？'
          ]
        },
        {
          name: '想你了',
          messages: [
            '我也在想你呢，好想抱抱你～',
            '我们很快就能见面啦！',
            '我数着日子等见你呢',
            '想我的时候就给我发消息吧',
            '距离产生美，但是我更想产生和你在一起的回忆'
          ]
        }
      ]
    }
  },

  computed: {
    currentMessage() {
      if (!this.currentMood) return ''
      return this.currentMood.messages[this.currentMessageIndex]
    }
  },

  methods: {
    selectMood(mood) {
      this.currentMood = mood
      this.currentMessageIndex = 0
      this.loveCount = 0
    },

    showNextMessage() {
      this.currentMessageIndex = 
        (this.currentMessageIndex + 1) % this.currentMood.messages.length
    },

    resetMood() {
      this.currentMood = null
      this.currentMessageIndex = 0
      this.loveCount = 0
    },

    increaseLove() {
      if (this.loveCount < 10) {
        this.loveCount++
      }
    }
  }
}
</script>

<style scoped>
.comfort-container {
  max-width: 600px;
  margin: 20px auto;
  padding: 20px;
  text-align: center;
  background-color: #fff5f5;
  border-radius: 15px;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
}

.header {
  margin-bottom: 30px;
  color: #ff4b6b;
}

.mood-selection {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
  justify-content: center;
  margin-bottom: 30px;
}

.mood-btn {
  padding: 12px 24px;
  border: none;
  border-radius: 20px;
  background-color: #ff8da1;
  color: white;
  cursor: pointer;
  transition: all 0.3s ease;
}

.mood-btn:hover {
  background-color: #ff4b6b;
  transform: scale(1.05);
}

.message-box {
  background-color: white;
  padding: 20px;
  border-radius: 10px;
  margin: 20px 0;
  font-size: 18px;
  color: #ff4b6b;
  min-height: 60px;
}

.action-buttons {
  display: flex;
  gap: 15px;
  justify-content: center;
  margin: 20px 0;
}

.action-btn {
  padding: 10px 20px;
  border: none;
  border-radius: 15px;
  background-color: #ff8da1;
  color: white;
  cursor: pointer;
  transition: all 0.3s ease;
}

.action-btn:hover {
  background-color: #ff4b6b;
}

.love-meter {
  margin-top: 30px;
}

.hearts {
  margin: 15px 0;
  font-size: 24px;
}

.heart {
  margin: 0 2px;
  animation: pulse 1s infinite;
}

.love-btn {
  padding: 8px 16px;
  border: none;
  border-radius: 15px;
  background-color: #ff4b6b;
  color: white;
  cursor: pointer;
  transition: all 0.3s ease;
}

.love-btn:hover {
  background-color: #ff3355;
}

@keyframes pulse {
  0% { transform: scale(1); }
  50% { transform: scale(1.1); }
  100% { transform: scale(1); }
}
</style>