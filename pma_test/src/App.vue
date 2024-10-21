<template>
  <div v-for="message in messages" :key="message.id"
       :class="{message_gpt:message.sender==='GPT',message_user:message.sender!=='GPT'}">
    <p>
      {{ message.sender }}: {{ message.body }}
    </p>
  </div>
  <input v-model="chatMessage" v-on:keyup.enter="sendMessage" class="chat-input" placeholder="input text">
</template>

<script>

import axios from "axios";


export default {

  name: 'App',
  data() {
    return {
      chatMessage: "",
      messages: [],
    }
  },
  methods: {
    sendMessage() {
      let message = {
        sender: "Igor",
        body: this.chatMessage,
        id: this.messages.length + 1
      }
      this.messages.push(message)
      this.chatMessage = ""

    },
    async fetchMessages() {
      const response = await axios.get()
      this.messages.push(response.data)
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.chat-input {
  position: fixed;
  bottom: 40px;
  left: 40px;
  right: 40px;
  outline: 2px solid purple;
  padding: 20px;
  font-size: 20px;
  box-sizing: border-box;

}

.message_user {
  outline: 1px solid cadetblue;
  padding: 10px;
  margin-left: 100px;
  margin-right: 100px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5); /* Добавляем тень для объёмности */
  margin-top: 10px;
  text-align: left;
}

.message_gpt {
  outline: 1px solid palevioletred;
  padding: 10px;
  margin-left: 100px;
  margin-right: 100px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5); /* Добавляем тень для объёмности */
  margin-top: 10px;
  text-align: right;
}

</style>
