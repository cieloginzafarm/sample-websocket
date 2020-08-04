<template>
  <div id="app">
    <h2>Trying out Ayame Lite</h2> 
    <button v-on:click="sendMessage('You have successfully sent a message')">Send Message</button>
  </div>
</template>

<script>
export default {
  name: 'App',
  data: function() {
    return {
      connection: null
    }
  },
  methods: {
    sendMessage: function(message) {
      console.log(message)
      console.log(this.connection);
      this.connection.send(message);
    }
  },
  created: function() {
    console.log("Starting connection to Ayame Lite Server")
    this.connection = new WebSocket("wss://ayame-lite.shiguredo.jp/signaling", "cielojordanjp@test-ayame")
    this.connection.onmessage = function(event) {
      console.log(event);
    }

    this.connection.onopen = function(event) {
      console.log(event)
      console.log("Successfully connected to the Ayame lite websocket server...")
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
</style>
