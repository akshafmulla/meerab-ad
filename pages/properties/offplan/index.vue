<template>
    <v-layout column justify-center class="grey lighten-4">
        <v-container class="ma-15">
            <p class="text-center display-1 font-weight-light">OFFPLAN PROJECTS</p>
            <v-row>
                <v-col cols="12" sm="12" md="4" xl="3" class="d-flex" v-for="(data,index) in projects" :key="index">
                    <v-card flat class="rounded-lg mx-2" :to="`/properties/offplan/${getName(data.property_name)}`" style="cursor : pointer;" elevation="0">
                        <v-img :src="data.src" height="275"></v-img>
                        <p class="pt-4 px-3 font-weight-bold mb-1">{{data.property_name}}</p>
                        <v-row class="px-5">
                            <v-col cols="12" sm='12' md="6">
                                <p class="mb-1 caption"><v-icon size="18" class="mt-n1" color="primary">mdi-office-building-marker-outline</v-icon>&emsp;{{data.location}}</p>
                                <p class="mb-1 caption"><v-icon size="18" class="mt-n1" color="primary">mdi-home-city-outline</v-icon>&emsp;{{data.property_type}}</p>
                            </v-col>
                            <v-col cols="12" sm='12' md="6">
                                <p class="mb-1 caption"><v-icon size="18" class="mt-n1" color="primary">mdi-shield-home-outline</v-icon>&emsp;{{data.builder_name}}</p>
                                <p class="mb-1 caption"><v-icon size="18" class="mt-n1" color="primary">mdi-warehouse</v-icon>&emsp;<span v-for="(item, i) in data.rooms" :key="i">{{item}} <span v-if="i < data.rooms.length - 1">,&nbsp;</span> </span></p>
                            </v-col>
                        </v-row>
                    </v-card>
                </v-col>
            </v-row>
        </v-container>
        
        <!-- <v-btn class="primary" @click="addProperty" dark>Add Project</v-btn> -->
    </v-layout>
</template>

<script>
export default {
    data(){
        return{
            properties:[],
            projects: [
                {location:'Creek Harbour',property_type:'Building',builder_name:'Emaar',rooms:[3,4],src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/Banner.jpg',property_name:'Creek Horizon at Dubai Creek Harbour'},
                {location:'Arabian Ranches 3',property_type:'Building',builder_name:'Emaar',rooms:[3,4],src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Caya/Banner.JPG',property_name:'Caya at Arabian Ranches 3 by Emaar'},
                {location:'Arabian Ranches',property_type:'Building',builder_name:'Emaar',rooms:[3,4],src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Aseel/Banner.JPG',property_name:'Aseel at Arabian Ranches by Emaar'},
                {location:'Downtown Dubai',property_type:'Building',builder_name:'Emaar',rooms:[3,4],src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Opera+Grand/Banner.JPG',property_name:'Opera Grand at Downtown Dubai by Emaar'},
                {location:'Creek Harbour',property_type:'Building',builder_name:'Emaar',rooms:[3,4],src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/Banner.jpg',property_name:'Creek Horizon at Dubai Creek Harbour by Emaar'},
                {location:'Creek Harbour',property_type:'Building',builder_name:'Emaar',rooms:[3,4],src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Harbour+Gate/Banner.jpg',property_name:'Harbour Gate at Dubai Creek Harbour by Emaar'},
                {location:'Dubai Hills Estate',property_type:'Building',builder_name:'Emaar',rooms:[3,4],src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Mulberry/Banner.jpg',property_name:'Mulberry at Dubai Hills Estate by Emaar'},
            ],
        }
    },
    mounted(){
        this.onload()
    },
    methods:{
        async onload(){
            await this.$axios.$get('properties/all')
            .then(res=>{
                this.properties = res
            })
            .catch(e => console.log(e))

        },
        getName(val){
            return val.replace(/\s/g,'-')
        },
        addProperty(){
            let projects = {
                property_name:'Creek Horizon at Dubai Creek Harbour',
                location:'Creek Harbour',
                property_type:'Building',
                builder_name:'Emaar',
                rooms:[3,4],
                banner_img:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/creek-horizon/2.JPG',
                property_pics:[],
                property_details:{}
            }

            this.$axios.$post('properties/add-item/', projects).then(res=>console.log(res)).catch(e => console.log(e))

        }
    },
    computed:{
        
    }
}
</script>