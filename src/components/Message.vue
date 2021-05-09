<template>
    <div class='message' :class='message.by'>
        <img class='user-img' v-if="message.by === 'teacher'" src='./../assets/teacher.png'/>
        <p>{{ message.text }}
            <small>{{ message.date }}</small>
        </p>
        <img class="user-img" v-if="message.by === 'student'" src="./../assets/student.png"/>
    </div>
</template>

<script>
    export default {
        name: 'Message',
        props: ['message']
    }
</script>

<style scoped lang="scss">
    .message {
        display: flex;
        align-content: center;
        margin: 1rem 0;

        p {
            margin: 0 1rem;
            padding: .5rem 1rem;
            border-radius: .3rem;
            max-width: 84%;

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
            margin-top: .5rem;
            width: 2.4rem;
            height: 2.4rem;
            border-radius: 2rem;
        }
    }

</style>