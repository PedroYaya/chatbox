<template>
    <div class='input-container'>
        <input type='text' v-model='message' @keyup.enter='send'>
        <a class='send-btn' @click='send'>
            <img src='./../assets/send.png'/>
        </a>
    </div>
</template>

<script>
    export default {
        name: 'ChatInput',
        data() {
            return {
                message: ''
            }
        },
        methods: {
            send() {
                this.$emit('send', this.message)
                this.message = ''
            }
        }
    }
</script>

<style scoped lang='scss'>
    .input-container {
        display: flex;
        align-items: center;
        border-top: 1px solid #d2cfcf;
        padding: 1.3rem .7rem;

        input {
            line-height: 2.3rem;
            width: 100%;
            border: none;
            padding: 0 1rem;
            background: #f7f7f7;
            border-radius: 1.5rem;
            border: .05rem solid #bfbfbf;
        }

        .send-btn {
            display: flex;
            justify-content: center;
            align-items: center;
            background: #0B8CFA;
            width: 2.7rem;
            height: 2.4rem;
            border-radius: 2rem;
            margin: 0 .5rem 0 1rem;

            @media (min-width: 1024px) {
                width: 2.5rem;
            }

            img {
                width: 1.5rem;
                height: 1.5rem;
            }
        }

    }

    *:focus {
        outline: none;
    }
</style>
