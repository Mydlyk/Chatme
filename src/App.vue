<template>
  <div id="app">
    <Header />
    <ChatWindow :messages="messages" />
    <UserInput @send="sendMessage" />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import ChatWindow from "./components/ChatWindow.vue";
import UserInput from "./components/UserInput.vue";
import { Ollama } from 'ollama'
export default {
  name: "App",
  components: {
    Header,
    ChatWindow,
    UserInput,
  },
  data() {
    return {
      messages: [],
      
    };
  },
  methods: {
    
    async sendMessage(message) {
      this.messages.push({ text: message, sender: "user" });
      try {
        const response = await this.sendToGPT(message);
        this.updateMessages(response);
      } catch (error) {
        console.error("Błąd podczas komunikacji z API GPT:", error);
        this.updateMessages("Błąd podczas komunikacji z API GPT:" + error);
      }
    },
    async sendToGPT(message) {
      try {
      const modelfile = `
            FROM mistral
            SYSTEM "Your job is to answer questions contextually and accurately."
            `
        const ollama = new Ollama({ host: 'http://localhost:11434' })

        const response = await ollama.chat({
          model: 'mistral',
          messages: [{ role: 'user', content: message+" Answer this question in Polish",modelfile: modelfile }], stream: true
        });
        return response;
      } catch (error) {
        throw error;
      }
    },
    async updateMessages(response) {
  let lastMessageIndex = this.messages.length - 1; 
  for await (const part of response) {
    
    if (lastMessageIndex >= 0 && this.messages[lastMessageIndex].sender === "bot") {
      this.messages[lastMessageIndex].text += part.message.content; 
    } else {
      
      this.messages.push({ text: part.message.content, sender: "bot" });
      lastMessageIndex++; 
    }
  }
},
  },
};
</script>

<style>

</style>
