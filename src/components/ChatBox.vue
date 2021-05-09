<template>
  <section class="chat-box">
    <div class="list-container" ref="chatbox">
      <ul class="list">
        <li v-for="(message, idx) in messages" :key="idx">
          <Message v-if="message.type === 'message'" :message="message"/>
          <File v-if="message.type === 'file'" :message="message"/>
        </li>
      </ul>
    </div>
    <ChatInput v-on:send="send($event)"/>
  </section>
</template>

<script>
import Message from "./Message";
import File from "./File";
import ChatInput from "./ChatInput";
import Json from "./../../db.json";

export default {
  name: 'ChatBox',
  components: {
    Message,
    File,
    ChatInput
  },
  data() {
    return {
      messages: Json.messages
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.$refs.chatbox.scrollTop = this.$refs.chatbox.scrollHeight
    })
  },
  methods: {
    send(message) {

      if (message !== '') {

        const date = new Date();
        this.messages.push({
          text: message,
          by: 'student',
          date: date.toDateString(),
          type: 'message'
        })

        const BASE_URL = 'https://dummyapi.io/data/api'
        const APP_ID = '6094e0f7ae6d813da0908e7b'
        const POST_ID = 'UWdcOFTc7DfzOhI6LpI4'

        this.$axios.get(`${BASE_URL}/post/${POST_ID}`, { headers: { 'app-id': APP_ID } })
                .then(res => {

                  this.messages.push({
                    text: res.data.text,
                    by: 'teacher',
                    date: date.toDateString(),
                    type: 'message'
                  })
                  this.$nextTick(() => {
                    this.$refs.chatbox.scrollTop = this.$refs.chatbox.scrollHeight
                  })
                })
      }
    }
  }

}
</script>

<style scoped lang="scss">

  .chat-box, .list {
    display: flex;
    flex-direction: column;
    list-style-type: none;
  }

  .list-container {
    position: relative;
    max-height: 500px;
    overflow: scroll;
  }

  .list {
    padding: .5rem;
  }
</style>