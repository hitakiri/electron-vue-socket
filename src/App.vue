<template>
  <div id="app">
    <h2>Hello</h2>
    <button @click="sendMessage()">Send message</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      ws: null
    };
  },
  created() {
    console.log("Start app...");
    this.ws = new WebSocket("ws://localhost:8081/ws");
    this.ws.onopen = function(event) {
      console.log(event);
      console.log("Удачное подключение к вебсокету");
    };

    this.ws.onmessage = function(event) {
      console.log("Полученны данные из вебсокета");
      console.log(event);
    };
  },
  methods: {
    sendMessage: function() {
      console.log(this.ws);
      let message = { name: "hey", data: "some data" };
      let rawData = JSON.stringify(message);
      this.ws.send(rawData);
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
