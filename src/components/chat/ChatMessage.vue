<template>
    <v-card :color="msg.isRobot ? '' : 'rgb(54, 89, 255)'"
            style="border-radius: 8px;"
            width="fit-content"
            class="mb-5"
            :style="{'margin-left': msg.isRobot ? '' : 'auto'}"
    >
        <!-- message text -->
        <v-card-text  :style="{'color': msg.isRobot ? 'black' : 'white'}" class="pa-2">
            {{msg.message}}
        </v-card-text>
    </v-card>
</template>

<script>
    export default {
        name: "ChatMessage",
        props: ["msg"]
    }
</script>

<style scoped>

</style>
