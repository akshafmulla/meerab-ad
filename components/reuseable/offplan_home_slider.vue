<template>
    <div class="mx-sm-n5 mx-lg-15">
        <v-sheet class="mx-auto grey lighten-4" elevation="0">
            <v-slide-group cycle class="pa-4 mx-auto" show-arrows>
                <v-slide-item v-for="(item,i) in items" :key="i" class="text-center">
                    <v-card  class="ma-4" flat :to="`/properties/offplan/${getName(item.property_name)}`" style="cursor : pointer;">
                        <v-img :src="item.banner_img" :height="windowSize ? '150' : '300'" :width="windowSize ? '160' : '320'">
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
            // items: [
            //     {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/Banner.jpg',property_name:'Creek Horizon at Dubai Creek Harbour'},
            //     {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Caya/Banner.JPG',property_name:'Caya at Arabian Ranches 3 by Emaar'},
            //     {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Aseel/Banner.JPG',property_name:'Aseel at Arabian Ranches by Emaar'},
            //     {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Opera+Grand/Banner.JPG',property_name:'Opera Grand at Downtown Dubai by Emaar'},
            //     {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/Banner.jpg',property_name:'Creek Horizon at Dubai Creek Harbour by Emaar'},
            //     {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Harbour+Gate/Banner.jpg',property_name:'Harbour Gate at Dubai Creek Harbour by Emaar'},
            //     {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Mulberry/Banner.jpg',property_name:'Mulberry at Dubai Hills Estate by Emaar'},
            // ],
            items:[]
        }
    },
    mounted(){
        this.onload()
    },
    methods:{
        getName(val){
            return val.replace(/\s/g,'-')
        },
        async onload(){
            await this.$axios.$get('properties/offplan/all')
            .then(res=>{
                this.items = res
            })
            .catch(e => console.log(e))
        },
    },
    computed:{
        windowSize(){
            return this.$vuetify.breakpoint.mobile ? true : false
        }
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