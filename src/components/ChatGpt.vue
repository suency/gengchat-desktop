<script setup lang="ts">
import { ref, reactive, onMounted } from 'vue'
import Loading from './Loading.vue'
import axios from 'axios'
defineProps<{ msg: string }>()

let showLoading = ref(false)
let chattext = ref('')
const count = ref(0)

onMounted(() => {
  const payload = {
    text: chattext.value
  };
  /* axios.post('https://api.daezi.cloud/chatgpt', payload)
    .then(response => {
      console.log(response.data);
    })
    .catch(error => {
      console.error(error);
    }); */
})
const chatList = reactive({
  data: [
    {
      content: 'Welcome to GengChat',
      left: true
    }
  ]
})

function getData(content: string, left: boolean) {
  return {
    content,
    left
  }
}

function send() {
  if (chattext.value === '') {
    alert("Content can not be empty!")
    return
  }

  chatList.data.push(getData(chattext.value, false))
  showLoading.value = true
  const payload = {
    text: chattext.value
  };
  axios.post('https://api.daezi.cloud/chatgpt', payload)
    .then(response => {
      showLoading.value = false
      chattext.value = ''
      chatList.data.push(getData(response.data.content.replace(/\n/g,""), true))
      console.log(response.data);
    })
    .catch(error => {
      console.error(error);
    });
  // showLoading.value = true
  // console.log(chattext.value)
}
</script>

<template>
  <!-- <h1>{{ msg }}</h1> -->
  <div>
    <Loading class="myLoading" v-show="showLoading"></Loading>
    <div class="convo" data-from="Sonu Joshi">
      <ul class="chat-thread">
        <li :class="{ left: item.left, right: !item.left }" v-for="(item, index) in chatList.data" :key="index">{{
          item.content
        }}</li>
      </ul>

    </div>
    <div class="content">
      <button @click="send()">Send</button>
      <textarea v-model="chattext" placeholder="Please input what you want to ask?"></textarea>
    </div>
  </div>
</template>

<style scoped>
.myLoading {
  position: fixed;
  top: 0;
  z-index: 11;
}

.convo {
  width: 90vw;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  height: 72vh;
  overflow-y: scroll;
  overflow-x: hidden;
  padding: 20px;
}

.content {
  display: flex;
  flex-direction: column;
  position: fixed;
  bottom: 20px;
  z-index: 10;
}

.content button {
  background-color: rgba(25, 147, 147, 0.1);
  margin-bottom: 10px;
  color: #0EC879;
  width: 100px;
  align-self: flex-end;
}

.content button:hover {
  border: 1px solid #0EC879;
  outline: none !important;
}

.content button:focus {
  outline: none !important;
}

.content textarea {
  resize: none;
  width: 90vw;
  height: 52px;
  border: none;
  background-color: rgba(25, 147, 147, 0.1);
  border-radius: 10px;
  color: #0EC879;
  padding: 15px;
  box-sizing: border-box;
  font-size: 18px;
}

.content textarea:focus {
  outline: none !important;
  border-color: #0EC879;
  /* box-shadow: 0 0 10px #0EC879; */
}

.content textarea::placeholder {
  font-size: 18px;
  opacity: 0.6;
}


.convo ul {
  width: 100%;
}

.chat-thread li {
  max-width: 450px;
}

.chat-thread li.right {
  animation: show-chat-odd 0.15s 1 ease-in;
  -moz-animation: show-chat-odd 0.15s 1 ease-in;
  -webkit-animation: show-chat-odd 0.15s 1 ease-in;
  float: right;
  margin-right: 80px;
  color: #0AD5C1;
  text-align: left;
  word-break: break-all;
}

.chat-thread li.right:before {
  right: -80px;
  background-image: url(../assets/me.png);
  background-size: contain;
}

.chat-thread li.right:after {
  border-right: 15px solid transparent;
  right: -15px;
}

.chat-thread li.left {
  animation: show-chat-even 0.15s 1 ease-in;
  -moz-animation: show-chat-even 0.15s 1 ease-in;
  -webkit-animation: show-chat-even 0.15s 1 ease-in;
  float: left;
  margin-left: 80px;
  color: #0EC879;
  text-align: left;
  word-break: break-all;
}

.chat-thread li.left:before {
  left: -80px;
  background-image: url(../assets/you.png);
  background-size: contain;
}

.chat-thread li.left:after {
  border-left: 15px solid transparent;
  left: -15px;
}

::-webkit-scrollbar {
  width: 10px;
}

::-webkit-scrollbar-track {
  border-radius: 10px;
  background-color: rgba(25, 147, 147, 0.1);
}

::-webkit-scrollbar-thumb {
  border-radius: 10px;
  background-color: rgba(25, 147, 147, 0.2);
}

.chat-thread {
  margin: 24px auto 0 auto;
  padding: 0 20px 0 0;
  list-style: none;
  /*   overflow-y: scroll;
  overflow-x: hidden; */
}

.chat-thread li {
  position: relative;
  clear: both;
  display: inline-block;
  padding: 16px 20px 16px 20px;
  margin: 0 0 20px 0;
  font: 16px/20px 'Noto Sans', sans-serif;
  border-radius: 10px;
  background-color: rgba(25, 147, 147, 0.2);
}

/* Chat - Avatar */
.chat-thread li:before {
  position: absolute;
  top: 0;
  width: 50px;
  height: 50px;
  border-radius: 50px;
  content: '';
}

/* Chat - Speech Bubble Arrow */
.chat-thread li:after {
  position: absolute;
  top: 15px;
  content: '';
  width: 0;
  height: 0;
  border-top: 15px solid rgba(25, 147, 147, 0.2);
}


.chat-window {
  position: fixed;
  bottom: 18px;
}

.chat-window-message {
  width: 100%;
  height: 48px;
  font: 32px/48px 'Noto Sans', sans-serif;
  background: none;
  color: #0AD5C1;
  border: 0;
  border-bottom: 1px solid rgba(25, 147, 147, 0.2);
  outline: none;
}



@keyframes show-chat-even {
  0% {
    margin-left: -480px;
  }

  100% {
    margin-left: 0;
  }
}

@-moz-keyframes show-chat-even {
  0% {
    margin-left: -480px;
  }

  100% {
    margin-left: 0;
  }
}

@-webkit-keyframes show-chat-even {
  0% {
    margin-left: -480px;
  }

  100% {
    margin-left: 0;
  }
}

@keyframes show-chat-odd {
  0% {
    margin-right: -480px;
  }

  100% {
    margin-right: 0;
  }
}

@-moz-keyframes show-chat-odd {
  0% {
    margin-right: -480px;
  }

  100% {
    margin-right: 0;
  }
}

@-webkit-keyframes show-chat-odd {
  0% {
    margin-right: -480px;
  }

  100% {
    margin-right: 0;
  }
}

.credits {
  text-align: center;
  margin-top: 35px;
  color: rgba(255, 255, 255, 0.35);
  font-family: 'Noto Sans', sans-serif;
}

.credits a {
  text-decoration: none;
  color: rgba(255, 255, 255, 0.35);
}
</style>
