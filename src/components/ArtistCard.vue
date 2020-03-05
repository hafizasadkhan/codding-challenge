<template>
    <v-card
            class="text-left"
            max-width="344"
            shaped=""
    >
        <v-card-text>
            <v-container fluid>
                <v-row>
                    <v-col cols="8">
                        <v-list-item-title class="headline mb-1">{{artist.name}}</v-list-item-title>
                        <v-subheader>{{artist.facebook_page_url}}</v-subheader>
                    </v-col>
                    <v-col cols="4">
                        <v-list-item-avatar
                                tile
                                size="80"
                                color="grey"
                        >
                            <v-img :src="artist.thumb_url"></v-img>

                        </v-list-item-avatar>

                    </v-col>
                </v-row>
            </v-container>

        </v-card-text>
    </v-card>
</template>
<script>
    export default {
        name:'artist-card',
        props:['artist']
    }
</script>
<style>

</style>
