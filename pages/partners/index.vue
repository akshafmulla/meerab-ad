<template>
    <div class="">
        <BannerImage image_url="https://meerabproperties.s3.ap-south-1.amazonaws.com/Static/sobha.jpg" :gradiantFlag="true" :textFlag="false" />
        <p class="text-center display-1 font-weight-light primary--text mt-5">SOBHA REALTY</p>
        <v-container class="mx-10">
            <h3>Sobha Hartland offers the most luxurious and exclusive lifestyle. A sought-after residential space in the heart of Dubai, this freehold community is home to a vast expanse of greenery. Residents of Sobha Hartland live a posh upmarket life and come home to peace and tranquillity.</h3>
        </v-container>
        <p class="text-center display-1 font-weight-light primary--text mt-5">CONTACT US</p>
        <v-layout column align-center justify-center>
            <v-row justify="center" align="center">
                <v-col cols="12" sm="12" >
                    <ContactUS />
                </v-col>
            </v-row>
        </v-layout>
    </div>
</template>

<script>
import ContactUS from '~/components/reuseable/contact-us-form'
import BannerImage from '~/components/reuseable/bannerImage'

export default {
    components: {
       ContactUS,BannerImage
    },
    data(){
        return{

        }
    },
    mounted(){

    },
    methods:{

    },
    computed:{
        
    }
}
</script>