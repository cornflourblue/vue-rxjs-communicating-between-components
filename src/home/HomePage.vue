<template>
    <div>
        <h2>Vue.js + RxJS Component Communication</h2>
        <button @click="sendMessage()" class="btn btn-primary">Send Message</button>
        <button @click="clearMessages()" class="btn btn-secondary">Clear Messages</button>
    </div>
</template>

<script>
import { messageService } from '@/_services';

export default {
    methods: {
        sendMessage() {
            // send message to subscribers via observable subject
            messageService.sendMessage('Message from Home Page Component to App Component!');
        },
        clearMessages() {
            // clear messages
            messageService.clearMessages();
        }
    }
};
</script>