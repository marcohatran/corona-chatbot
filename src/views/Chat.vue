<template>
    <v-card
            tile
            style="margin: auto;"
            max-width="400px"
            min-height="500px"
            class="mt-12"
    >
        <v-row class="header pa-0 ma-0" >
            <v-col align="center" class=" pt-7">
                <v-avatar
                        width="70px"  height="70px"
                        tile
                        color="white"
                        class="mt-3 avatarRobot"
                >
                    <v-icon size="50" color="rgb(54, 89, 255)">mdi-robot</v-icon>
                </v-avatar>
            </v-col>

            <v-btn icon class="mt-3 mr-2">
                <v-icon color="white">mdi-dots-vertical</v-icon>
            </v-btn>
        </v-row>

        <v-card-text class="chats" >
            <chat-message v-for="(msg, index) in answers" :msg="msg" :key="index"/>
            <div class="typing-indicator" v-if="isTyping">
                <span></span>
                <span></span>
                <span></span>
            </div>
        </v-card-text>

        <v-card-actions>
            <v-text-field v-model="chatText"
                          @keydown.enter="sendMessage"
                          hide-details
                          dense
                          tile
                          label="Send message..."
                          outlined
                          color="rgb(54, 89, 255)"
                          class="mb-3 ml-3"
            />
            <v-btn @click="sendMessage" icon class="ml-2 mr-3 mb-3">
                <v-icon size="32"color="rgb(54, 89, 255)">mdi-send</v-icon>
            </v-btn>
        </v-card-actions>
    </v-card>
</template>

<script>
    import ChatMessage from "../components/chat/ChatMessage";

    import {enviroment} from "../enviroments/enviroment";
    import { ApiAiClient } from 'api-ai-javascript'
    const token = enviroment.dialogflow.clientBot;
    const baseURL = enviroment.dialogflow.path;

    const client = new ApiAiClient({accessToken: token})

    export default {
        name: "Chat",
        components: {
            "chat-message": ChatMessage
        },
        data: () => ({
            chatText: "",
            answers: [],
            isTyping: false,
        }),
        methods: {

             sendMessage() {

                 const userMessage = {
                     isRobot: false,
                     message:  this.chatText
                 };

                 this.answers.push(userMessage);
                 this.isTyping = true;
                client.textRequest(this.chatText).then((response) => {
                    console.log("response", response)

                    const dataRobot = {
                        isRobot: true,
                        message: response.result.fulfillment.speech
                    };

                    this.answers.push(dataRobot);
                    this.chatText = '';
                    this.isTyping = false;
                })
            }
        }
    }
</script>

<style scoped>
    .header {
        height: 70px;
        background-color: rgb(54, 89, 255);
    }

    .avatarRobot {
        box-shadow: 0px 3px 1px -2px rgba(0, 0, 0, 0.2), 0px 2px 2px 0px rgba(0, 0, 0, 0.14), 0px 1px 5px 0px rgba(0, 0, 0, 0.12);
        border-radius: 4px;
        position: absolute;
        z-index: 4;
    }

    .chats {
        height: 500px;
        overflow-y: scroll;
        padding-top: 70px
    }

    .typing-indicator {
        will-change: transform;
        width: auto;
        border-radius: 50px;
        padding: 10px;
        display: table;
        animation: 2s bulge infinite ease-out;
        background-color: #F5F5F5;
    }

    span {
        height: 7px;
        width: 7px;
        float: left;
        margin: 0 1px;
        background-color: #9E9EA1;
        border-radius: 50%;
        opacity: 0.4;
    }

    .typing-indicator span:nth-child(1)
    {
        animation: 1s blink infinite .3333s;
    }

    .typing-indicator span:nth-child(2)
    {
        animation: 1s blink infinite .6666s;
    }

    .typing-indicator span:nth-child(3)
    {
        animation: 1s blink infinite .9999s;
    }

    @keyframes blink
    {
        50%
        {
            opacity: 1;
        }
    }

    @keyframes pulse
    {
        50% {
            transform: scale(1.05);
        }
    }
</style>
