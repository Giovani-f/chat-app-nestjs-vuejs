<script setup>
  import { io } from 'socket.io-client'
  import { onBeforeMount, ref } from 'vue';

  const socket = io('http://localhost:3000');

  const messages = ref([]);
  const messageText = ref('');
  const joined = ref(false);
  const name = ref('');
  const typingDisplay = ref('');

  onBeforeMount(() => {
   socket.emit('findAllMessages', {}, res => {
    messages.value = res;
   })

   socket.on('message', message => {
    messages.value.push(message);
   })
  });

  const join = () => {
   socket.emit('join', {
    name: name.value,
   }, () => {
    joined.value = true;
   });
  }

  const sendMessage = () => {
   socket.emit('createMessage', {
    text: messageText.value,
   }, () => {
    messageText.value = '';
   });
  }

  socket.on('typing', data => {
   if (data.isTyping) {
    typingDisplay.value = `${data.name} is typing...`;
   } else {
    typingDisplay.value = '';
   }
  });

  let timeout;
  const emmitTyping = () => {
   socket.emit('typing', {
    isTyping: true, name: name.value
   });
   clearTimeout(timeout);
   timeout = setTimeout(() => {
    socket.emit('typing', {
     isTyping: false, name: name.value
    });
   }, 2000);
  }
</script>

<template>
  <div class="chat">
    <div v-if="!joined">
      <form @submit.prevent="join">
        <label>Whats your name?</label>
        <input v-model="name" placeholder="Name" />
        <button type="submit">Join</button>
      </form>
    </div>
    <div class="chat-container" v-else>
      <div class="message-container">
        <div v-for="message in messages" v-bind:key="message.text">
      [{{ message.name }}]: {{ message.text }}</div>
      </div>
    </div>

    <div class="message-input" v-if="joined">

      <div v-if="typingDisplay">
    {{ typingDisplay }}</div>

    <hr />
      <form @submit.prevent="sendMessage">
        <input v-model="messageText" @input="emmitTyping" placeholder="Message" />
        <button type="submit">Send</button>
      </form>
    </div>
  </div>
</template>

<style scoped>
@import './assets/base.css';

.chat {
  padding: 20px;
  height: 100vh;
}

.chat-container {
  display: flex;
  flex-direction: column;
  height: 80%;
}

.message-container {
  flex: 1;
}
</style>
