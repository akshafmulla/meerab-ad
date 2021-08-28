<template>
    <div>
        <v-img src="https://meerabproperties.s3.ap-south-1.amazonaws.com/precondo-ca-OlSGcrLSYkw-unsplash.jpg" cover height="500"></v-img>
        <TravelPackage />
        <InvestWithUs />
        <p class="text-center display-1 font-weight-light">CONTACT US</p>

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
import TravelPackage from '~/components/reuseable/travel_package'
import InvestWithUs from '~/components/reuseable/invest_with_us'
import ContactUS from '~/components/reuseable/contact-us-form'

export default {
    components: {
        InvestWithUs,TravelPackage,ContactUS
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