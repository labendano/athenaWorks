<template>
    <v-flex class="user-card" xs6>
        <v-list-tile
              :key="position"
              avatar
            >
              <v-list-tile-avatar>
                <img :src="getPic('s')">
              </v-list-tile-avatar>

              <v-list-tile-content>
                <v-list-tile-title v-html="formatName"></v-list-tile-title>
                <v-list-tile-sub-title v-html="email"></v-list-tile-sub-title>
              </v-list-tile-content>
        </v-list-tile>
        <v-divider></v-divider>
    </v-flex>
</template>

<script>
export default {
    name: 'UserItem',
    props: ['name', 'email', 'picture', 'position'],
    computed: {
        formatName: function(){
            return this.capitalizeFirst(this.name.title) +" "+ this.capitalizeFirst(this.name.first) +" "+ this.capitalizeFirst(this.name.last);
        }
    },
    methods: {
        capitalizeFirst: function(string) {
            return string.charAt(0).toUpperCase() + string.slice(1);
        },
        getPic: function(size) {
            switch (size){
                case 's':
                    return this.picture.thumbnail;
                break;
                case 'm':
                    return this.picture.medium;
                break;
                case 'l':
                    return this.picture.large;
                break;
                default:
                    return this.picture.medium;
                break;
            }
        }
    }
}
</script>

<style>
</style>