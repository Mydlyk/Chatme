<template>
  <div class="user-input">
    <input type="text" v-model="message" @keyup.enter="sendMessage" placeholder="Wpisz swoją wiadomość..." />
    <button @click="sendMessage">></button>
  </div>
</template>

<script>
export default {
  name: "UserInput",
  data() {
    return {
      message: "",
    };
  },
  methods: {
    async sendMessage() {
      if (this.message.trim() !== "") {
        this.$emit("send", this.message);
        this.message = "";
      }
    },
  },
};
</script>


