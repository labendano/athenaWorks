<template>
    <!-- <div  v-if="this.index>-1">{{getUser.name}}</div> -->
    <v-layout>
    <v-flex v-if="this.index>-1" xs12 offset-sm3>
        <v-card>
            <v-img
            class="white--text"
            height="200px"
            :src="getUser.picture.large"
            >
            <v-container fill-height fluid>
                <v-layout fill-height>
                <v-flex xs12 align-end flexbox>
                    <span class="headline">{{formatName(getUser.name)}}</span>
                </v-flex>
                </v-layout>
            </v-container>
            </v-img>
            <v-card-title>
                <div class="user-data">
                    <span class="grey--text">Gender</span>
                    <span class="headline">{{getUser.gender}}</span>
                    <span class="grey--text">Location</span>
                    <span class="headline">{{capitalizeFirst(getUser.location.city)}}, {{capitalizeFirst(getUser.location.state)}}</span>
                    <span class="grey--text">Phone</span>
                    <span class="headline">{{getUser.phone}}</span>
                </div>
            </v-card-title>
        </v-card>
        </v-flex>
    </v-layout>
</template>

<script>
export default {
    name: 'UserCard',
    props: ['users-data'],
    data: function () {
        return {
            index: -1,
        }
    },
    methods:{
        capitalizeFirst: function(string) {
            return string.charAt(0).toUpperCase() + string.slice(1);
        },
        formatName: function(name){
            return this.capitalizeFirst(name.first) +" "+ this.capitalizeFirst(name.last);
        }
    },
    computed: {
        getUser: function(){
            if(this.index >- 1){
                return this.usersData[this.index];
            }
        },
    }
}
</script>

<style>
    .user-data span{
        width: 100%;
        float: left;
        text-align: left;
    }
</style>
