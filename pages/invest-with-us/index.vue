<template>
    <div class="">
        <BannerImage image_url="https://meerabproperties.s3.ap-south-1.amazonaws.com/vip_package/og.jpg" />
        <TravelPackage />
        <!-- <InvestWithUs /> -->
        <p class="text-center display-1 font-weight-light">TRAVEL PACKAGE INCLUDES</p>
        
        <v-container>
            <v-row class="px-10" justify="center">
                <v-col cols="12" sm="6" md="3" lg="3" xl="3" class="text-center" v-for="(data,index) in invest_cards" :key="index">
                    <v-hover v-slot="{ hover }">
                        <v-card class="rounded-xl" flat color="grey lighten-4" min-height="150" max-width="600" >
                            <div class="my-auto">
                                <p class="text-center pt-8"><v-icon size="30">{{data.icon}}</v-icon></p>
                                <v-divider class="mx-10 my-2"></v-divider>
                                <p class="font-weight-bold">{{data.name}}</p>
                                <v-expand-transition>
                                    <div v-if="hover" class="d-flex transition-fast-in-fast-out primary v-card--reveal white--text rounded-xl" style="height: 100%;">
                                        {{data.desc}}
                                    </div>
                                </v-expand-transition>
                            </div>
                        </v-card>
                    </v-hover>
                </v-col>
            </v-row>
        </v-container>

        <p class="text-center display-1 font-weight-light pt-6">CONTACT US</p>
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
import BannerImage from '~/components/reuseable/bannerImage'

export default {
    components: {
        InvestWithUs,TravelPackage,ContactUS,BannerImage
    },
    data(){
        return{
            invest_cards:[
                {icon:'mdi-helicopter',name:'PRIVATE TOUR',desc:'Experience Dubai and view our properties'},
                {icon:'mdi-bed-outline',name:'ACCOMMODATION',desc:'You will stay at one of our luxury hotels'},
                {icon:'mdi-passport',name:'UAE VISAS',desc:'We will arrange your UAE visit visa'},
                {icon:'mdi-airplane',name:'RETURN AIRFARES',desc:'Provided from your local airport to Dubai'},
                {icon:'mdi-handshake-outline',name:'TRAVEL CONCIERGE',desc:'We take care of everything'},
                {icon:'mdi-account-outline',name:'AIRPORT WELCOME',desc:'A personal welcome upon arrival'},
                {icon:'mdi-car-sports',name:'HOTEL TRANSFERS',desc:'We transfer you via our luxury cars'},
                {icon:'mdi-cash-plus',name:'DISCOUNTS',desc:'Enjoy exclusive investor privileges'},
                // {icon:'mdi-currency-usd',name:'Returns in US Dollars',desc:' Strong and consistent cash returns pegged to US Dollars'},
                // {icon:'mdi-cash-plus',name:'Investor Benefit',desc:'One of the highest ROI in the world'},
                // {icon:'mdi-handshake-outline',name:'Hassle-Free Experience',desc:'A bespoke approach to customer service'},
                // {icon:'mdi-helicopter',name:'Exclusive Tour for Investors',desc:'An investment visit to Dubai to explore our properties'},
            ],
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

<style>
.v-card--reveal {
  align-items: center;
  bottom: 0;
  justify-content: center;
  /* opacity: .5; */
  position: absolute;
  width: 100%;
}
</style>