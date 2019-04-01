<template>
    <div class="jumbotron">
        <div class="container text-center">
            <div class="row">
                <div class="col-sm-8 offset-sm-2">
                    <div v-for="(message, index) in messages" :key="index" class="alert alert-success">{{message.text}}</div>
                    <router-view></router-view>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { messageService } from '@/_services';

export default {
    name: 'app',
    data () {
        return {
            messages: []
        };
    },
    created () {
        // subscribe to home component messages
        this.subscription = messageService.getMessage().subscribe(message => {
            if (message) {
                // add message to local state if not empty
                this.messages.push(message);
            } else {
                // clear messages when empty message received
                this.messages = [];
            }
        });
    },
    beforeDestroy () {
        // unsubscribe to ensure no memory leaks
        this.subscription.unsubscribe();
    }
};
</script>