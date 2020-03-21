<template>
    <v-card
            tile
            style="margin: auto;"
            max-width="400px"
            min-height="400px"
            class="mt-12"
    >
        <v-row class="header pa-0 ma-0">
            <v-col align="center" class="pl-12 ml-5 pt-7">
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
            <chat-message/>
        </v-card-text>

        <v-card-actions>
            <v-text-field v-model="chatText"
                          hide-details
                          dense
                          tile
                          label="Send message..."
                          outlined
                          color="rgb(54, 89, 255)"
                          class="mb-6 ml-3"
            />
            <v-btn @click="sendMessage" icon class="ml-2 mr-3 mb-6">
                <v-icon size="32"color="rgb(54, 89, 255)">mdi-send</v-icon>
            </v-btn>
        </v-card-actions>
    </v-card>
</template>

<script>
    import ChatMessage from "../components/chat/ChatMessage";

    export default {
        name: "Chat",
        components: {
            "chat-message": ChatMessage
        },
        data: () => ({
            chatText: ""
        }),
        methods: {
            sendMessage() {

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
    }

    .chats {
        height: 400px;
        overflow-y: scroll;
        padding-top: 70px
    }
</style>
