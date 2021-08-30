<template>
    <div class="mx-15 py-4">
        <p class="text-center display-1 font-weight-light">OFFPLAN PROJECTS</p>
        <v-sheet class="mx-auto grey lighten-4" elevation="0">
            <v-slide-group cycle class="pa-4" show-arrows>
                <v-slide-item v-for="(item,i) in items" :key="i" class="text-center">
                    <v-card  class="ma-4" flat :to="`/properties/offplan/${getName(item.property_name)}`" style="cursor : pointer;">
                        <v-img :src="item.src" height="300" width="320">
                            <p class="mb-0 text-h6 white--text">{{item.property_name}}</p>
                        </v-img>
                    </v-card>
                </v-slide-item>
            </v-slide-group>
        </v-sheet>
    </div>
</template>

<script>

export default {
    
    data(){
        return{
            toggle_multiple:1,
            items: [
                {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/Banner.jpg',property_name:'Creek Horizon at Dubai Creek Harbour'},
                {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Caya/Banner.JPG',property_name:'Caya at Arabian Ranches 3 by Emaar'},
                {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Aseel/Banner.JPG',property_name:'Aseel at Arabian Ranches by Emaar'},
                {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Opera+Grand/Banner.JPG',property_name:'Opera Grand at Downtown Dubai by Emaar'},
                {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/Banner.jpg',property_name:'Creek Horizon at Dubai Creek Harbour by Emaar'},
                {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Harbour+Gate/Banner.jpg',property_name:'Harbour Gate at Dubai Creek Harbour by Emaar'},
                {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Mulberry/Banner.jpg',property_name:'Mulberry at Dubai Hills Estate by Emaar'},
            ],
        }
    },
    mounted(){},
    methods:{
        getName(val){
            return val.replace(/\s/g,'-')
        },
    },
    computed:{

    }
}
</script>

<style scoped>
    .searchCard{
        background: rgba(0,0,0,.6);
        padding: 15px 15px 8px;
        border-radius: 5px;
    }
</style>