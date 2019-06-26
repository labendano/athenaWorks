<template>
    <v-app>
        <v-container grid-list-lg text-xs-center>
            <v-layout row wrap>
                <v-flex xs7>
                    <v-layout row wrap>
                        <v-flex xs12>
                            <v-card>
                                <v-card-title class="headline font-weight-regular red white--text">Users</v-card-title>
                                <v-card-text>
                                    <v-subheader class="pa-0">Name to search?</v-subheader>
                                    <v-autocomplete
                                    v-if="userCards.length > 0"
                                    :items = "userCards"
                                    :loading="isLoading"
                                    hide-no-data
                                    autofocus
                                    :search-input.sync="search"
                                    :item-text = "userIndexes"
                                    placeholder="Start typing to Search"
                                    prepend-icon="mdi-database-search"
                                    return-object
                                    >
                                    <template v-slot:append-outer>
                                        <v-slide-x-reverse-transition
                                        mode="out-in"
                                        >
                                        </v-slide-x-reverse-transition>
                                    </template>
                                    </v-autocomplete>
                                </v-card-text>
                            </v-card>
                        </v-flex>
                                <user-item v-for="(user, index) in info" :position="index" :key="index" :id="index" :name="user.name" :email="user.email" :picture="user.picture"
                                @click.native="showCard(index)">
                                </user-item>
                    </v-layout>
                </v-flex>
                <v-flex xs5>
                    <user-card id="card" ref="maincard" :index="-1" :users-data="info"></user-card>
                </v-flex>
            </v-layout>
        </v-container>
    </v-app>
</template>

<script>
    import axios from 'axios';
    import UserItem from '../components/UserItem';
    import UserCard from '../components/UserCard';
    import regeneratorRuntime from 'regenerator-runtime'
    export default {
    name: 'App',
    components: {UserItem, UserCard},
    data () {
            return {
                userCards: [],
                userIndexes: [],
                info: null,
                search : null,
                cont : 0,
                isLoading : false,
                }
        },
    methods: {
        showCard: function(number){
            this.$refs.maincard.index = number;
            this.isLoading = false;
        },
    },
    computed:{
        formatData: async function() {
            let arrCards = [];
            let arrIndex = [];
            let cont = 0 ;
            const user = await axios.get('https://randomuser.me/api/?results=13')
            this.info=user.data.results;
            this.info.forEach(function(element, index) {
                arrCards.push(element.name.first.charAt(0).toUpperCase() + element.name.first.slice(1) + " " + element.name.last.charAt(0).toUpperCase() + element.name.last.slice(1));
                arrIndex.push(cont);
                cont++;
            });
            this.userCards = arrCards;
            this.userIndexes = arrIndex;
        },
    },
    watch: {
        search (val) {
            this.isLoading = true; 
            this.showCard(this.userCards.indexOf(val));
        },
    },
    mounted () {
        this.formatData;
    },
}
</script>

<style scoped>
</style>