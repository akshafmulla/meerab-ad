<template>
    <v-layout column justify-center class="">
        <v-container class="pa-5">

            <p class="text-center display-1 font-weight-light">{{community_name}} Projects</p>
            <v-row>
                <v-col cols="12" sm="12" md="4" xl="3" class="d-flex" v-for="(data,index) in projects" :key="index">
                    <v-card flat class="rounded-lg mx-2 grey lighten-4" :to="`/properties/offplan/${getName(data.property_name)}`" style="cursor : pointer;" elevation="0">
                        <v-img :src="data.banner_img" cover :height="windowSize ? '175' : '275'"></v-img>
                        <p class="pt-4 px-3 font-weight-bold mb-1">{{data.property_name}}</p>
                        <v-row class="pa-5">
                            <v-col cols="12" sm='12' md="6" class="py-0">
                                <p class="mb-1 caption"><v-icon size="18" class="mt-n1" color="primary">mdi-office-building-marker-outline</v-icon>&emsp;{{data.community}}</p>
                                <p class="mb-1 caption"><v-icon size="18" class="mt-n1" color="primary">mdi-home-city-outline</v-icon>&emsp;{{data.property_type}}</p>
                            </v-col>
                            <v-col cols="12" sm='12' md="6" class="py-0">
                                <p class="mb-1 caption"><v-icon size="18" class="mt-n1" color="primary">mdi-shield-home-outline</v-icon>&emsp;{{data.developer}}</p>
                                <p class="mb-1 caption"><v-icon size="18" class="mt-n1" color="primary">mdi-warehouse</v-icon>&emsp;<span v-for="(item, i) in data.rooms" :key="i">{{item}}<span v-if="i < data.rooms.length - 1">,&nbsp;</span> </span> Rooms</p>
                            </v-col>
                        </v-row>
                    </v-card>
                </v-col>
            </v-row>
        </v-container>
        
    </v-layout>
</template>

<script>
export default {
    data(){
        return{
            projects:[],
            community_name:''
        }
    },
    mounted(){
        this.onload()
    },
    methods:{
        async onload(){
            this.community_name =this.$route.params.id.replace(/-/g,' ')
            await this.$axios.$get('properties/communities/'+this.$route.params.id.replace(/-/g,' '))
            .then(res=>{
                console.log(res)
                this.projects = res
            })
            .catch(e => console.log(e))
        },
        getName(val){
            return val.replace(/\s/g,'-')
        },
        
    },
    computed:{
        windowSize(){
            return this.$vuetify.breakpoint.mobile ? true : false
        }
    }
}
</script>