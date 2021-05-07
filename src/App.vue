<template>
  <div id="app">
    <Modal/>

    <div style="display:none;">
      <ChatBox/>
    </div>
  </div>
</template>

<script>
import ChatBox from './components/ChatBox.vue'
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: {
    ChatBox,
    Modal
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
