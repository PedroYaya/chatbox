<template>
    <div>
        <b-button class="header" variant="primary" v-b-modal.chat>Open Chat</b-button>
        <b-modal id="chat" title="Comentarios" >
            <ChatBox/>
        </b-modal>
    </div>
</template>
<script>
import { BModal, VBModal } from 'bootstrap-vue'
import ChatBox from "./ChatBox";

export default {
    name: 'Modal',
    components: {
        BModal,
        ChatBox
    },
    directives: { 'b-modal': VBModal },
}
</script>

<style lang="scss">

    .modal-dialog {
        width: 90vw;
        max-width: 700px !important;
        background: white;
        border: .1rem solid red;
        border-radius: .3rem;
        margin: 1rem auto;
        justify-content: space-between;
    }

    .modal-header {
        position: relative;
        border-bottom: .2rem solid black;
        justify-content: center !important;
        border-bottom: .2rem solid black !important;

        button {
            position: absolute;
            right: 1rem;
            background: none;
            color: #0B8CFA;
            border: none;
            font-size: 2rem;
        }
    }

    .modal-body {
        padding: 0 !important;
    }

    .modal-footer {
        display: none !important;
    }
</style>