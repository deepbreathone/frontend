<template>
  <div id="app">
    <form
      class="chat"
      @submit="onSubmit"
    >
      <div class="chat-bubbles">
        <Bubble
          v-for="(message, index) in messages"
          :key="index"
          :msg="message.text"
          :isUserMessage="message.isUserMessage"/>
        <TypingIndicator v-if="isTyping" />
      </div>
      <input type="text" class="chat-input" v-model="message" placeholder="Your message here.." />
    </form>
  </div>
</template>

<script>
import Bubble from './components/Bubble.vue';
import TypingIndicator from './components/TypingIndicator.vue';

export default {
  name: 'App',
  components: {
    Bubble,
    TypingIndicator
  },
  data:() => {
    return {
      message: "",
      messages: [],
      isTyping: false
    }
  },
  mounted() {
    this.messages.push({
      text: "Welcome, how can I help you?",
      isUserMessage: false
    });
  },
  methods:{
    onSubmit(e) {
      e.preventDefault();
      this.messages.push({
        text: this.message,
        isUserMessage: true
      });
      
      this.message = "";
      this.generateAnswerMessage();
    },
    generateAnswerMessage() {
      this.isTyping = true;
      setTimeout(() => {
        this.isTyping = false;
        this.messages.push({
          text: "One moment please, thinking :)",
          isUserMessage: false
        });
      }, 1000);
    }
  }
}
</script>

<style lang="scss">
*, *:before, *:after {
  box-sizing: border-box;
}

body {
  margin: 0;
  width: 100vw;
  height: 100vh;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 100%;
  height: 100%;
  background-image: url(https://raw.githubusercontent.com/deepbreathone/instagram/master/quotes/background/deep_dreath_crop.png);
  background-position: center center;
  background-size: cover;
  display: flex;
  align-items: center;
  justify-content: center;
}

.chat {
  width: 100%;
  height: 100%;
  background: #fff;
  border: 1px solid #1a1a1a;
  padding: 20px 35px;
  -webkit-box-shadow: 1px 1px 40px 5px rgba(0,0,0,0.4);
  box-shadow: 1px 1px 40px 5px rgba(0,0,0,0.4);
  display: flex;
  flex-direction: column;

  @media (min-width: 768px) {
    width: 60%;
    height: 500px;
    border-radius: 5px;
  }
}

.chat-bubbles {
  clear: both;
  display: flex;
  flex-direction: column;
}

.chat-input {
  font-size: 16px;
  float: left;
  width: 347px;
  height: 40px;
  padding: 0 10px;
  color: #1a1a1a;
  border: 0;
  outline: none;
  background-color: #eceff1;
  font-family: 'Source Sans Pro', sans-serif;
  font-weight: 400;
  margin-top: auto;
  width: 100%;
}
</style>
