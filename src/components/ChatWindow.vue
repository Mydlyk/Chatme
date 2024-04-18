<template>
  <div class="chat-container">
    <div class="chat-window">
      <div v-for="(message, index) in messages" :key="index" :class="['message', message.sender]">
        <div class="messages-display">
        <span v-if="message.sender === 'user'">
         User: 
        </span>
        <span v-else>
       Ai: 
        </span>
        {{ message.text }}
      </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ChatWindow",
  props: {
    messages: {
      type: Array,
      required: true,
    },
  },
};
</script>


