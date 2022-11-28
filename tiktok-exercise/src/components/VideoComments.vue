<script setup>

import { ref, reactive, onMounted } from 'vue'

let chatMessages = reactive( { chatMessages: [] } );
let message = ref("");

function postMessages() {
    document.querySelector(".form__button").addEventListener("click", function() {
        console.log("clicked");
        let message = document.querySelector(".form__input").value;
        let sender = "John Doe";
        let receiver = "Jane Doe";
        let date = new Date();

        const apiUrl = "https://nodejs-chatapp-ricky.onrender.com/api/v1/messages";
        fetch(apiUrl, {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify({
                    message: message,
                    sender: sender,
                    receiver: receiver,
                    date: date,
            }),
        })
            .then((response) => response.json())
            .then((data) => {
                chatMessages.chatMessages.push({
                    message: message,
                    sender: sender,
                    receiver: receiver,
                    date: date,
                });
                document.querySelector(".form__input").value = "";
            });        
    });
};

onMounted(() => {
    const apiUrl = "https://nodejs-chatapp-ricky.onrender.com/api/v1/messages";
    fetch(apiUrl)
        .then((response) => response.json())
        .then((data) => {
            chatMessages.chatMessages = data.data.messages;
        });
    postMessages();
});

</script>

<template>
    <div class="commentSection">
        <h2>Comments</h2>
        <div class="messagesContainer">
            <div class="message"  v-for="c in chatMessages.chatMessages" v-bind:key="c._id">
                <h3 class="message__sender">{{ c.sender }}</h3>
                <p class="message__text">{{ c.message }}</p>
            </div>
        </div>
        <div class="form">
            <input type="text" name="message" class="form__input" id="messageInput" placeholder="Comment">
            <button class="form__button">Send</button>
        </div>
    </div>
</template>

<style scoped>

.commentSection {
    padding: 0 1em;
    height: 100%;
    margin: 0;
    height: 85%;
    border: 1px solid #ccc;
}

.messagesContainer {
    overflow-y: scroll;
    padding: 0 1em;
    height: 60vh;
    margin: 0;
}

.message {
    padding: .1em 1rem .5em 1rem;
    margin: .2rem 0;
    background-color: #fec6df;
    border-radius: 8px;
}

.message__sender {
    font-weight: bold;
    color: black;
}

.message__text {
    margin: 0;
    padding-left: 1em; 
}

.form {
    padding: .5em 1em;
}

.form__input {
    width: 70%;
    padding: .5em;
    border: 1px solid #ccc;
    border-radius: 8px;
}

.form__button {
    padding: .5em 1em;
    border: 1px solid #ccc;
    border-radius: 8px;
    background-color: #fec6df;
    color: #111;
    font-weight: bold;
    margin-left: 1em;
}

.form__button:hover {
    background-color: #ec83c5;
    color: white;
    cursor: pointer;
}

</style>
