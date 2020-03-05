<template>
    <div>

        <v-container fluid="">
            <v-text-field
                    v-model="search"
                    label="Search Artist"
                    outlined
                    clearable
            ></v-text-field>

            <v-spacer></v-spacer>
            <v-btn
                    color="primary"
                    @click="searchArtist"
            >
                Search
                <v-icon right>search</v-icon>
            </v-btn>

        </v-container>

        <!-- Result card -->
        <v-card class="mt-3">
            <v-card-title class="headline ">
                Search Results
            </v-card-title>
            <v-card-text>
                <v-container fluid="">
                    <artist-card v-if="artist"
                    :artist="artist"
                    ></artist-card>
                </v-container>
            </v-card-text>
            <v-divider></v-divider>
            <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn
                        :disabled="!model"
                        color="grey darken-3"
                        @click="model = null"
                >
                    Clear
                    <v-icon right>mdi-close-circle</v-icon>
                </v-btn>
            </v-card-actions>
        </v-card>
    </div>
</template>
<script>
    import axios from 'axios'
    import ArtistCard from "../components/ArtistCard";

    export default {
        name: 'search-artist',
        components: {ArtistCard},
        data() {
            return {
                descriptionLimit: 60,
                // artist: {"thumb_url":"https://s3.amazonaws.com/bit-photos/thumb/8267376.jpeg","mbid":"8ef964a0-c730-455e-bc05-43e5a6f6269d","facebook_page_url":"http://www.facebook.com/55715582584","image_url":"https://s3.amazonaws.com/bit-photos/large/8267376.jpeg","name":"Maroon","options":{"display_listen_unit":false},"id":"13042","tracker_count":10031,"upcoming_event_count":0,"url":"https://www.bandsintown.com/a/13042?came_from=267&app_id=app_id"},
                artist: null,
                isLoading: false,
                model: null,
                search: '',
                first: ''
            }
        },

        computed: {
            fields() {
                if (!this.model) return []

                return Object.keys(this.model).map(key => {
                    return {
                        key,
                        value: this.model[key] || 'n/a',
                    }
                })
            },
            items() {
                return this.artist.map(entry => {
                    const Description = entry.Description.length > this.descriptionLimit
                        ? entry.Description.slice(0, this.descriptionLimit) + '...'
                        : entry.Description

                    return Object.assign({}, entry, {Description})
                })
            },
        },
        methods:{
            searchArtist(){
                axios
                    .get('https://rest.bandsintown.com/artists/' + this.search + '?app_id=app_id')
                    .then(response => {
                        (console.log(response))
                        this.artist = response.data
                        console.log(JSON.stringify(this.artist))
                    })
            }
        },
        watch: {
            search() {

                if(this.search !== '')
                {
                    console.log("");
                    // this.searchArtist(this.search)
                }
                else{
                    this.artist = null
                }
            },
        },
    }
</script>
