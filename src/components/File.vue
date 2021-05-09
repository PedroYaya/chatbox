<template>
    <div class='file'>
        <div>
            <h6>{{ message.version }}</h6>
            <p>{{ message.name }}</p>
            <div>
                <span>{{ message.file.type }}</span>
                <span class='size'>{{ message.file.size }}</span>
                <span class='date'>{{ message.date }}</span>
            </div>
        </div>
        <a :href='message.url' target='_blank'>
            <img class='download-img' src='./../assets/download.png'/>
        </a>
    </div>
</template>

<script>
    export default {
        name: 'File',
        props: ['message']
    }
</script>

<style scoped lang="scss">
    .file {
        display: flex;
        justify-content: space-between;
        text-align: left;
        border-top: .1rem solid #80808040;
        border-bottom: .1rem solid #80808040;
        padding: 1rem;

        h4 {
            margin: 0;
        }

        h6 {
            text-transform: uppercase;
        }

        p {
            margin: .5rem 0;
            color: #0B8CFA;
            font-weight: 500;
        }

        span {
            font-size: .9rem;
        }

        .size, .date {
            margin-left: .5rem;
        }

        .download-img {
            cursor: pointer;
            width: 2.5rem;
            padding: .2rem;
            border-radius: 2rem;
            margin-top: 1rem;
        }
    }

</style>