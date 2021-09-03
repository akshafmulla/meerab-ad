<template>
    <div>
        <v-img src="https://meerabproperties.s3.ap-south-1.amazonaws.com/Static/thank-you.jpg" cover :gradient="gradiantFlag ? 'to top right, rgba(100,115,201,.33), rgba(25,32,72,.7)' : ''" v-if="!windowSize">
            <v-container bg fill-height grid-list-md text-xs-center >
                <v-layout row wrap align-center>
                    <v-flex>
                        <p :class="windowSize ? 'display-1' : 'display-3'" class="white--text font-weight-bold">Thank You for reaching out.</p>
                        <p :class="windowSize ? 'display-1' : 'display-3'" class="white--text font-weight-bold">We will get back to you soon.</p>
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
        <v-container bg fill-height grid-list-md text-xs-center v-if="windowSize">
            <v-layout row wrap align-center>
                <v-flex >
                    <div class="pt-15  text-center ">
                        <p><v-icon class="" color="green" size="35">mdi-check-circle</v-icon></p>
                        <p class="display-1 font-weight-bold" style="color : #af880a;">THANK YOU</p>
                        <p class="caption " >We Thank you for your interest. We will get back to you soon.</p>
                        <p class="mt-3"><v-btn @click="back" class="grey--text mr-3" text small outlined>back</v-btn><v-btn class="primary" dark small to="/properties/offplan">Offplan Properties</v-btn></p>
                    </div>
                </v-flex>
            </v-layout>
        </v-container>
        
    </div>
</template>

<script>

export default {
    components: {
    },
    data(){
        return{
            gradiantFlag : true
        }
    },
    mounted(){

    },
    methods:{
        back(){
            this.$router.go(-1)
        }
    },
    computed:{
        windowSize(){
            return this.$vuetify.breakpoint.mobile ? true : false
        }
    }
}
</script>