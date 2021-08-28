<template>
    <div class="ma-15">
        <v-layout column align-center justify-center >
            <!-- <v-container class="" > -->
                <v-card class="rounded-lg white mt-n3 mx-15" flat max-width="1200">
                    <v-row align="center">
                        <v-col cols="12" sm="12" md="6" class="travelCard pa-8 rounded-xl">
                            <p class="display-1 font-weight-light">VIP TRAVEL PACKAGES FOR INVESTORS</p>
                            <p class="caption font-italic">On your private investment tour, feel inspired to invest in Dubai's finest properties</p>
                            <v-btn large @click="redirect" v-if="redirectButton"> More info</v-btn>
                        </v-col>
                        <v-col cols="12" sm="12" md="6" class="pa-8">
                            <p class="caption">The Dubai Investment Visit is a special vacation package for investors looking to profit from Dubai's expanding real estate market.</p>
                            <p class="caption">We would like to invite you to be our special guest on this tour, which will include private viewings of Dubai's top developers and exciting investment opportunities in The Meerab Properties' property portfolio.</p>
                            <p class="caption">Take advantage of this once-in-a-lifetime opportunity to diversify your financial portfolio by purchasing a property from Meerab Properties.</p>
                        </v-col>
                    </v-row>
                </v-card>
            <!-- </v-container> -->
        </v-layout>
    </div>
</template>

<script>

export default {
    
    data(){
        return{
            
        }
    },
    mounted(){},
    methods:{
        redirect(){
            return this.$route.path == '/' ? this.$router.push('/invest-with-us') : ''
        }
    },
    computed:{
        redirectButton(){
            return this.$route.path == '/' ? true : false
        }
    }
}
</script>

<style scoped>
    .travelCard{
        background-image: linear-gradient(to right, rgba(191,155,48,1), rgba(255,255,255,1));
    }
</style>