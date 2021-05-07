<template>
  <section class="chat-box">
    <div class="header">
      <h3>Comentarios</h3>
      <a>x</a>
    </div>
    <div class="list-container" ref="chatbox">
      <ul class="list">
        <li v-for="(message, idx) in messages" :key="idx">
          <Message v-if="message.type === 'message'" :message="message"/>
          <File v-if="message.type === 'file'" :message="message"/>
        </li>
      </ul>
    </div>
    <div class="inputs">
      <input type="text" v-model="message" @keyup.enter="send">
      <button @click="send">></button>
    </div>
  </section>
</template>

<script>
import Message from "./Message";
import File from "./File";

export default {
  name: 'ChatBox',
  components: {
    Message,
    File
  },
  data() {
    return {
      message: '',
      messages: [
        {
          version: 'Version 1',
          name: 'Title of my first work',
          file: {
            type: 'PDF Documnent',
            size: '2.5MB'
          },
          url: 'https://griersmusings.files.wordpress.com/2019/12/thecompleteguidetothetarot_bygray.pdf',
          type: 'file'
        },
        {
          text: 'primer mensaje',
          by: 'student',
          date: 'Fri May 07 2021',
          type: 'message'
        },
        {
          text: 'primer respuesta',
          by: 'teacher',
          date: 'Fri May 07 2021',
          type: 'message'
        },
        {
          text: 'primer mensaje',
          by: 'student',
          date: 'Fri May 07 2021',
          type: 'message'
        },
        {
          version: 'Version 2',
          name: 'Title of my second work',
          file: {
            type: 'PDF Documnent',
            size: '5.5MB'
          },
          url: 'https://griersmusings.files.wordpress.com/2019/12/thecompleteguidetothetarot_bygray.pdf',
          type: 'file'
        },
        {
          text: 'primer respuesta',
          by: 'teacher',
          date: 'Fri May 07 2021',
          type: 'message'
        }
      ]
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.$refs.chatbox.scrollTop = this.$refs.chatbox.scrollHeight
    })
  },
  methods: {
    send() {
      if (this.message !== '') {
        const date = new Date();

        this.messages.push({
          text: this.message,
          by: 'student',
          date: date.toDateString()
        })

        const BASE_URL = 'https://dummyapi.io/data/api'
        const APP_ID = '6094e0f7ae6d813da0908e7b'
        const POST_ID = 'UWdcOFTc7DfzOhI6LpI4'

        this.$axios.get(`${BASE_URL}/post/${POST_ID}`, { headers: { 'app-id': APP_ID } })
                .then(res => {

                  this.messages.push({
                    text: res.data.text,
                    by: 'teacher',
                    date: date.toDateString()
                  })
                  this.$nextTick(() => {
                    this.$refs.chatbox.scrollTop = this.$refs.chatbox.scrollHeight
                  })
                })
        this.message = ''
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

  .chat-box {
    width: 90vw;
    max-width: 700px;
    height: 100%;
    background: white;
    border: .1rem solid red;
    border-radius: .3rem;
    margin: 1rem auto;
    justify-content: space-between;
  }

  .header {
    position: relative;
    border-bottom: .2rem solid black;

    h3 {
      position: absolute;
      margin: .5rem;
      left: 1rem;
      right: 1rem;
      line-height: 2.5rem;
    }

    a {
      display: flex;
      justify-content: flex-end;
      font-size: 1.5rem;
      padding: .5rem 1rem;
      color: #0B8CFA;
      font-weight: 500;
    }
  }

  .list {
    padding: .5rem;

  }

  .inputs {
    display: flex;
    border-top: 1px solid #d2cfcf;
    padding: 1.3rem .7rem;

    input {
      line-height: 3;
      width: 100%;
      border: none;
      padding: 0 1rem;
      background: #f7f7f7;
      border-radius: 1.5rem;
      border: .05rem solid #bfbfbf;
    }

    button {
      background: #0B8CFA;
      color: white;
      border-radius: 3rem;
      border: none;
      cursor: pointer;
      font-size: 2rem;
      width: 3.2rem;
      font-weight: 900;
      margin: 0 .6rem;
    }

  }

  *:focus {
    outline: none;
  }
</style>
