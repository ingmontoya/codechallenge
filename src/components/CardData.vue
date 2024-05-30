<script setup>
defineProps({
    imageSrc: {
        type: String,
        required: true,
    },
    title: {
        type: String,
        required: true,
    }
})
</script>

<template>
    <v-card>
        <v-img :src="imageSrc" class="align-end" gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)" height="200px"
            cover>
            <v-card-title class="text-white" v-text="title"></v-card-title>
        </v-img>

        <v-card-actions>
            <v-spacer></v-spacer>

            <v-btn color="medium-emphasis" icon="mdi-heart" size="small"></v-btn>

            <v-btn color="medium-emphasis" icon="mdi-bookmark" size="small"></v-btn>

            <v-btn color="medium-emphasis" icon="mdi-share-variant" size="small"></v-btn>
        </v-card-actions>
    </v-card>
</template>