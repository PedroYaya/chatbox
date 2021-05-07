<template>
  <section class="chat-box">
    <div class="header">
      <h3>Comentarios</h3>
      <a>x</a>
    </div>
    <div class="list-container" ref="chatbox">
      <ul class="list">
        <li v-for="(message, idx) in messages" :key="idx">

          <div v-if="message.type === 'message'" class="message" :class="message.by">
            <img class="user-img" v-if="message.by === 'teacher'" src="./../assets/user.png"/>
            <p>{{ message.text }}
              <small>{{ message.date }}</small>
            </p>
            <img class="user-img" v-if="message.by === 'student'" src="./../assets/user.png"/>
          </div>

          <div v-if="message.type === 'file'" class="file-container">
            <div>
              <h4>{{ message.version }}</h4>
              <p>{{ message.name }}</p>
              <div>
                <span>{{ message.file.type }}</span>
                <span class="size">{{ message.file.size }}</span>
              </div>
            </div>
            <a :href="message.url" target=”_blank”>
              <img class="download-img" src="./../assets/download.png"/>
            </a>
          </div>

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
export default {
  name: 'ChatBox',
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

    .message {
      display: flex;
      align-content: center;
      margin: 1rem 0;

      p {
        margin: 0 1rem;
        padding: .5rem 1rem;
        border-radius: .3rem;

        small {
          display: block;
          text-align: left;
          font-size: .7rem;
        }
      }

      &.teacher {

        p {
          background: #fafafa;
        }
      }

      &.student {
        justify-content: flex-end;

        p {
          color: white;
          background: #0B8CFA;
        }
      }

      .user-img {
        background: #e8e8e8;
        padding: .4rem;
        width: 1.4rem;
        height: 1.4rem;
        border-radius: 2rem;
      }
    }
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

  .file-container {
    display: flex;
    justify-content: space-between;
    text-align: left;
    border-top: .1rem solid #80808040;
    border-bottom: .1rem solid #80808040;
    padding: 1rem;

    h4 {
      margin: 0;
    }

    p {
      margin: .5rem 0;
      color: #0B8CFA;
      font-weight: 900;
    }

    span {
      font-size: .9rem;
    }

    .size {
      margin-left: .5rem;
    }

    .download-img {
      cursor: pointer;
      width: 2rem;
      background: #badfff;
      padding: .2rem;
      border-radius: 2rem;
      margin-top: 1rem;
    }
  }
</style>
