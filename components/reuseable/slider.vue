<template>
    <div>
        <v-carousel cycle hide-delimiters>
            <v-carousel-item v-for="(item,i) in items" :key="i" :src="item.banner_img" :to="`/properties/offplan/${getName(item.property_name)}`" cover style="cursor : pointer;">
                <p class="white--text heading-1 pt-sm-2 pt-md-4 text-right" justify="center"><span class="rounded-lg black pa-4 pt-15">{{item.property_name}}</span></p>
            </v-carousel-item>
        </v-carousel>
        <div class="mt-n15" v-if="!windowSize">
            <v-layout column align-center justify-center >
                <v-card class="searchCard  rounded-lg white mt-n3 px-4" flat >
                    <v-btn-toggle v-model="toggle_multiple" color="yellow darken-1" group>
                        <v-btn class="rounded-lg px-3 mx-2" elevation="0" :value="1" text >Buy</v-btn>
                        <v-btn class="rounded-lg px-3 mx-2" elevation="0" :value="2" text >Rent</v-btn>
                        <v-btn class="rounded-lg px-3 mx-2" elevation="0" :value="3" text >Off Plan</v-btn>
                        <v-btn class="rounded-lg px-3 mx-2" elevation="0" :value="4" text >Short-Term</v-btn>
                        <v-btn class="rounded-lg px-3 mx-2" elevation="0" :value="5" text >Find Agents</v-btn>
                    </v-btn-toggle>
                    <v-autocomplete :items="configuration[0].neighbourhoodList" multiple class="mt-3 rounded-lg" placeholder="Search here...." outlined dense solo flat prepend-inner-icon="mdi-magnify" v-if="configuration.length > 0"></v-autocomplete>
                    <p class="mb-0 text-right mt-n2"><v-btn small>search</v-btn></p>
                </v-card>
            </v-layout>
        </div>
    </div>
</template>

<script>

export default {
    // layout:'dashboard',
    props:['configuration'],
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
        this.getData()
    },
    methods:{
        async getData(){
            await this.$axios.$get("properties/home/banner/keys")
            .then(res =>{
                this.items = res
            }).catch()
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

<style scoped>
    .searchCard{
        background: rgba(0,0,0,.6);
        padding: 15px 15px 8px;
        border-radius: 5px;
    }
    /* @media only screen and (max-width: 1904px) {
        .carousal-height {
            height : '500px' ;
        }
    }

    @media only screen and (min-width: 1905px) {
        .carousal-height {
            height : '900px' ;
        }
    } */
</style>