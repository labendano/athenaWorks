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
                                    :hint="'Enter a name above'"
                                    :items="userCards"
                                    :readonly="false"
                                    :label="`Name`"
                                    prepend-icon="mdi-city"
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
                                @click.native="showCard(index)" v-model="userCards">
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
    export default {
    name: 'App',
    components: {UserItem, UserCard},
    data () {
            return {
                info: null,
                userCards: []
                }
        },
    mounted () {
        axios
            .get('https://randomuser.me/api/?results=13')
            .then(response => (this.info = response.data.results/*, console.log(this.info)*/))
            
    },
    methods: {
        showCard: function(number){
            this.$refs.maincard.index = number;
        }
    },
    computed:{
        processData: function(){
            this.info.forEach(function(element, index) {
                this.userCards.push(formatAutocomplete(element.name))
                // console.log(this.userCards);
            });
        },
        formatAutocomplete: function(name){
            return this.capitalizeFirst(name.first) +" "+ this.capitalizeFirst(name.last);
        },
        capitalizeFirst: function(string) {
            return string.charAt(0).toUpperCase() + string.slice(1);
        }
    }
}
</script>

<style scoped>
  /* .container {
    width: 800px;
    margin: 50px auto;
    text-align: center;
  } */
</style>