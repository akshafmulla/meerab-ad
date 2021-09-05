<template>
    <div class="grey lighten-4">
        <v-img src="https://meerabproperties.s3.ap-south-1.amazonaws.com/Static/contact-us.jpg" cover>
            <v-container bg fill-height grid-list-md text-xs-center >
                <v-layout row wrap align-center>
                    <v-flex>
                        <p :class="windowSize ? 'display-1' : 'display-3'" class="white--text font-weight-bold">CONTACT US</p>
                        <v-tooltip top color="pink">
                            <template v-slot:activator="{ on, attrs }">
                                <v-btn class="mr-2" color='white'  fab dark small v-bind="attrs" v-on="on">
                                    <a href="https://www.instagram.com/meerabproperties/" style="text-decoration: none !important;"><v-icon color="pink" size="25">mdi-instagram</v-icon></a> 
                                </v-btn>
                            </template>
                        Instagram
                        </v-tooltip>
                        <v-tooltip top color="blue">
                            <template v-slot:activator="{ on, attrs }">
                                <v-btn class="mr-2" color='white'  fab dark small v-bind="attrs" v-on="on">
                                    <a href="https://www.facebook.com/profile.php?id=100072154745739" style="text-decoration: none !important;"><v-icon color="blue" size="25">mdi-facebook</v-icon></a> 
                                </v-btn>
                            </template>
                        Facebook
                        </v-tooltip>
                        <v-tooltip top color="blue">
                            <template v-slot:activator="{ on, attrs }">
                                <v-btn class="mr-2" color='white'  fab dark small v-bind="attrs" v-on="on">
                                    <a href="https://www.linkedin.com/in/meerab-properties" style="text-decoration: none !important;"><v-icon color="blue" size="25">mdi-linkedin</v-icon></a> 
                                </v-btn>
                            </template>
                        LinkedIn
                        </v-tooltip>
                        <v-tooltip top color="cyan">
                            <template v-slot:activator="{ on, attrs }">
                                <v-btn class="mr-2" color='white'  fab dark small v-bind="attrs" v-on="on">
                                    <a href="https://twitter.com/MeerabProperty" style="text-decoration: none !important;"><v-icon color="cyan" size="25">mdi-twitter</v-icon></a> 
                                </v-btn>
                            </template>
                        Twitter
                        </v-tooltip>
                    </v-flex>
                </v-layout>
            </v-container>
        </v-img>
        <div class="mt-md-n15 pb-10">
            <v-row>
                <v-col cols="12" sm="0" md="2" class="py-0"></v-col>
                <v-col class="py-0" cols="12" sm="12" md="8">
                    <v-card class="grey lighten-4 rounded-xl px-5" min-height="400" flat>
                        <v-row>
                            <v-col cols="12" sm="12" md="6">
                                <v-card class="rounded-xl mt-5 pa-6 text-center" min-height="390" flat>
                                    <v-row align="center" justify="center">
                                        <v-col cols="12" sm="12" md="3" class="my-auto text-center">
                                            <v-icon class="" size="50" color="primary">mdi-phone-in-talk-outline</v-icon>
                                        </v-col>
                                        <v-col cols="12" sm="12" md="9" class="text-md-left pt-5">
                                            <p class="mb-2">Call us directly at</p>
                                            <p class="blue-grey--text font-weight-bold text-h6"><a href="tel:971 589328227" style="text-decoration : none !important;">+971 589328227</a></p>
                                        </v-col>
                                        <v-col cols="12" sm="12" md="3" class="my-auto text-center">
                                            <v-icon class="" size="50" color="green">mdi-whatsapp</v-icon>
                                        </v-col>
                                        <v-col cols="12" sm="12" md="9" class="text-md-left pt-5">
                                            <p class="mb-2">Chat with us on</p>
                                            <p class="green--text font-weight-bold text-h6" @click="whatasppRoute">+971 589328227</p>
                                        </v-col>
                                    </v-row>
                                    <v-row class="pa-6">
                                        <v-col cols="1" sm="1" class="text-right my-auto pt-0 px-0 ">
                                            <v-img contain height="10" src="https://meerabproperties.s3.ap-south-1.amazonaws.com/Static/uae-flag.png" />
                                        </v-col>
                                        <v-col cols="11" sm="11" class=" py-0 px-md-0 text-md-left">
                                            <p class="caption mb-3 font-weight-bold">03, 1st Floor, F1RST MOTORS, DUBAI, UAE</p>
                                        </v-col>
                                        <v-col cols="1" sm="1" class="text-right my-auto pt-0 px-0 ">
                                            <v-img contain height="10" src="https://meerabproperties.s3.ap-south-1.amazonaws.com/Static/us-flag.png" />
                                        </v-col>
                                        <v-col cols="11" sm="11" class=" py-0 px-md-0  text-md-left">
                                            <p class="caption mb-3 font-weight-bold">924 US ROUTE 9, SUITE 200 SOUTH AMBOY, NEW JERSEY 08879, US</p>
                                        </v-col>
                                    </v-row>
                                </v-card>
                            </v-col>
                            <v-col cols="12" sm="12" md="6" class="">
                                <v-card class="rounded-xl white mt-5" flat>
                                    <!-- <p class="text-center display-1 font-weight-bold primary--text pt-5">CONTACT US</p> -->
                                    <ContactUS />
                                </v-card>
                            </v-col>
                        </v-row>
                    </v-card>
                </v-col>
            </v-row>
        </div>
    </div>
</template>

<script>
import ContactUS from '~/components/reuseable/contact-us-form'

export default {
    components: {
       ContactUS
    },
    data(){
        return{
            phone: '971589328227',
        }
    },
    mounted(){

    },
    methods:{
        whatasppRoute(){
            window.open('https://wa.me/'+ this.phone + '?text=' + encodeURI("Hello!"), '_blank')
        },
    },
    computed:{
        windowSize(){
            return this.$vuetify.breakpoint.mobile ? true : false
        }
    }
}
</script>