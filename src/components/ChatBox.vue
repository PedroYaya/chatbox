<template>
  <section class="chat-box">
    <div class="header">
      <h3>Comentarios</h3>
      <a>x</a>
    </div>
    <div class="list-container" ref="chatbox">
      <ul class="list">

        <div class="file-container">
          <div>
            <h4>VERSION 1</h4>
            <p>Titulo del archivo a subir</p>
            <div>
              <span>Document / PDF (4.4MB)</span>
              <span> 28 Dic 2020 / 15:33</span>
            </div>
          </div>
          <a>
            <img class="download-img" src="./../assets/download.png"/>
          </a>
        </div>


        <li class="message" :class="message.by"
            v-for="(message, idx) in messages" :key="idx">
            <img class="user-img" v-if="message.by === 'teacher'" src="./../assets/user.png"/>
            <p>{{ message.text }}</p>
            <img class="user-img" v-if="message.by === 'student'" src="./../assets/user.png"/>
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
          text: 'primer mensaje',
          by: 'student'
        },
        {
          text: 'primer respuesta',
          by: 'teacher'
        },
        {
          text: 'primer mensaje',
          by: 'student'
        },
        {
          text: 'primer respuesta',
          by: 'teacher'
        },
        {
          text: 'primer mensaje',
          by: 'student'
        },
        {
          text: 'primer respuesta',
          by: 'teacher'
        },
        {
          text: 'primer mensaje',
          by: 'student'
        },
        {
          text: 'primer respuesta',
          by: 'teacher'
        },
        {
          text: 'primer mensaje',
          by: 'student'
        },
        {
          text: 'primer respuesta',
          by: 'teacher'
        },
        {
          text: 'segundo mensaje',
          by: 'student'
        },
        {
          text: 'segunda mensaje',
          by: 'teacher'
        },
      ]
    }
  },
  methods: {
    send() {
      if (this.message !== '') {
        this.messages.push({
          text: this.message,
          by: 'student'
        })

        const BASE_URL = 'https://dummyapi.io/data/api'
        const APP_ID = '6094e0f7ae6d813da0908e7b'
        const POST_ID = 'UWdcOFTc7DfzOhI6LpI4'

        this.$axios.get(`${BASE_URL}/post/${POST_ID}`, { headers: { 'app-id': APP_ID } })
                .then(res => {
                  this.messages.push({
                    text: res.data.text,
                    by: 'teacher'
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
