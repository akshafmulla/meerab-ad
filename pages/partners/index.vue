<template>
    <div class="grey lighten-4">
        <v-img src= "https://meerabproperties.s3.ap-south-1.amazonaws.com/Static/june_hartland_estates_page-0016.jpg" cover gradient="to top right, rgba(100,115,201,.33), rgba(25,32,72,.7)">
            <v-container  >
                <v-layout row wrap align-center>
                    <v-flex>
                        <p :class="windowSize ? 'display-1 pt-5' : 'display-3 pt-15'" class="white--text font-weight-bold text-center ">SOBHA REALTY</p>
                        <p class="white--text text-center">Book at Sobha Hartland and your Dubai trip is on us.</p>
                    </v-flex>
                </v-layout>
            </v-container>
        </v-img>
        <v-container  >
            <v-layout row wrap align-center>
                <v-flex>
                    <p :class="windowSize ? 'display-1 pt-5' : 'display-3 pt-10'" class="text-center" style="color : #af880a;">SOBHA REALTY</p>
                    <p class="mb-5">Sobha Hartland offers the most luxurious and exclusive lifestyle. A sought-after residential space in the heart of Dubai, this freehold community is home to a vast expanse of greenery. Sobha Hartland is located within MBR City and is just minutes from Burj Khalifa and Downtown Dubai.</p>
                    <p class="pt-10 text-center display-1 font-weight-light">VIP TRAVEL PACKAGES FOR INVESTORS</p>
                    <v-row class="px-10" justify="center">
                        <v-col cols="12" sm="6" md="4" lg="2" class="text-center" v-for="(data,index) in invest_cards" :key="index">
                            <v-card class="grey lighten-4" flat>
                                <p class="text-center"><v-icon size="30">{{data.icon}}</v-icon></p>
                                <v-divider class="mx-10 mb-2 mt-n2"></v-divider>
                                <p class="font-weight-bold">{{data.name}}</p>
                                <p class="caption">{{data.desc}}</p>
                            </v-card>
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col cols="12" sm="12" md="5">
                            <v-img src="https://meerabproperties.s3.ap-south-1.amazonaws.com/Static/3.jpg" cover></v-img>
                        </v-col>
                        <v-col cols="12" sm="12" md="7">
                            <p class="font-weight-light display-1">An Unparalleled Lifestyle In The Heart Of Dubai.</p>
                            <p>
                            Inspiring lifestyle, comfort and luxury living in every detail, Sobha Hartland is an 8 million sq. ft waterfront community of luxurious apartments, beautiful villas, and high-end townhouses. Presenting, luxury homes that come with expanses of lush green spaces, world-class amenities and a slew of mouth-watering eateries, retail centres, and entertainment facilities.
                            </p>
                            <p>
                            Experience the new definition of luxury with Sobha Hartland. Dwell in Dubai’s only freehold community, situated in the iconic Mohammed Bin Rashid Al Maktoum City, minutes away from the Burj Khalifa.</p>
                        </v-col>
                    </v-row>
                </v-flex>
            </v-layout>
        </v-container>
        <v-row class="white text-center align-center" >
            <v-col sm="0" md="3"></v-col>
            <v-col>
                <v-img max-width="800" src="https://meerabproperties.s3.ap-south-1.amazonaws.com/Static/Sobha+Locations.jpg" ></v-img>
            </v-col>
            <v-col sm="0" md="3"></v-col>
        </v-row>
        
        <p class="white py-10 mb-0 text-center display-1 font-weight-light">LOCATION</p>
        <v-parallax height="600" class="gradient" src="https://meerabproperties.s3.ap-south-1.amazonaws.com/Static/sobha2.jpg" gradient=""></v-parallax>
        <div class="pt-15 white">
            <v-parallax height="600" class="gradient" src="https://meerabproperties.s3.ap-south-1.amazonaws.com/Static/parallax-sobha.jpg" gradient="">
                <v-layout row wrap align-center>
                    <v-flex>
                        <p :class="windowSize ? 'display-1 pt-5' : 'display-3 pt-10'" class="white--text text-center font-weight-bold">Why Invest In Dubai Now?</p>
                        <p class="text-center mb-0">If you want to make a sound investment in Dubai’s real estate market, don’t delay! Now is the ideal time! </p>
                        <p class="text-center">Low interest rates, economic stimulus funds by the government and a pro-business environment, Dubai’s economy is already bouncing back with a more stable real estate market and competitive prices.</p>
                        <v-layout row wrap align-center class="text-center">
                            <v-flex>
                                <ul class="white--text font-weight-bold" style="list-style: none;">
                                    <li>0% capital gains tax</li>
                                    <li>0% income tax</li>
                                    <li>4th most visited city in the world</li>
                                    <li>High capital appreciation & rental yields</li>
                                    <li>Residence visa options</li>
                                    <li>Mortgage finance facilities available</li>
                                </ul>
                            </v-flex>
                        </v-layout>
                    </v-flex>
                </v-layout>
            </v-parallax>
        </div>

        <div class="white pt-5">
            <p class="text-center display-1 font-weight-light primary--text pt-5 mb-n5">CONTACT US</p>
            <v-layout column align-center justify-center>
                <v-row justify="center" align="center">
                    <v-col cols="12" sm="12" >
                        <ContactUS />
                    </v-col>
                </v-row>
            </v-layout>
        </div>
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
            gradiantFlag: true,
            invest_cards:[
                {icon:'mdi-airplane',name:'Flight to Dubai',desc:'Airfare to Dubai for 2 pax'},
                {icon:'mdi-bed-outline',name:'Hotel Stay',desc:'3 days 2 nights stay for 2 pax'},
                {icon:'mdi-car-sports',name:'Premium Transport',desc:'Airport transfer in premium vehicle.'},
                {icon:'mdi-passport',name:'UAE Visa',desc:'UAE Visas for 2 pax'},
                {icon:'mdi-office-building',name:'Residential Access',desc:'Priority residential inventory access'},
                {icon:'mdi-airplane',name:'Happy Customers',desc:'Depart with a lifetime investment at sobha hartland'},
            ],
        }
    },
    mounted(){

    },
    methods:{

    },
    computed:{
        windowSize(){
            return this.$vuetify.breakpoint.mobile ? true : false
        }
    }
}
</script>

<style>
.gradient{
    background: rgba(100,115,201,.33);
    background: linear-gradient(90deg, rgba(100,115,201,.33), rgba(25,32,72,.7) 35%, rgba(100,115,201,.33) 100%);
}
</style>