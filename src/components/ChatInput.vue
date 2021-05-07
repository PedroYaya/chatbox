

<template>
    <div class="input-container">
        <input type="text" v-model="message" @keyup.enter="send">
        <button @click="send">></button>
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

<style scoped lang="scss">
    .input-container {
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
