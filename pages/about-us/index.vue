<template>
    <div class="mt-1">
        <BannerImage image_url="https://meerabproperties.s3.ap-south-1.amazonaws.com/vip_package/about+us.jpg" />
        <div class="grey lighten-4">
            <p class="pt-8 text-center display-1 font-weight-light">ABOUT US</p>
            <v-container>
                <p class="px-sm-4 px-lg-15">Meerab Properties is a trusted real estate agency that makes its clients’ dreams a reality. We are a Dubai based Real Estate Company specializing in residential, commercial and retail properties within the UAE. Our large portfolio of real estate in Dubai offers our discerning clients the opportunity to invest in one of the world's fastest growing real estate markets. </p>
                <br>
                <p class="px-sm-4 px-lg-15">What makes us unique from other real estate companies in Dubai is that we don’t offer services but we offer trust, care, and integrity to our clients and create value in their dreams. Over the years we are proud to be a recognized and respected name within the UAE real estate community.</p>
                <br>
                <p class="px-sm-4 px-lg-15"><b>"SERVICE YOU DESERVE WITH PEOPLE YOU TRUST"</b> Since 2013 Meerab Properties has been working as a team to provide our clients with the very best in real estate services. Whether you are looking to purchase, sell or relocate our office can assist you with all of your real estate needs. We are in the business of helping people realize their real estate dreams. </p>
            </v-container>
        </div>
        <div class="px-sm-4 px-lg-15 pt-5">
            <v-container>
                <v-row class="px-sm-4 px-lg-15">
                    <v-col cols="12" sm="12" md="4" class="my-auto text-center" v-for="(data,index) in cards" :key="index">
                        <v-icon size="120" color="primary">{{data.icon}}</v-icon>
                        <p class="pt-8 text-center display-1 font-weight-light">{{data.title}}</p>
                        <p>{{data.desc}}</p>
                    </v-col>
                </v-row>
            </v-container>
        </div>
        <div class="grey lighten-4">
            <p class="pt-8 text-center display-1 font-weight-light">OUR TEAM</p>
            <v-container>
                <v-row align="center" justify="center">
                    <v-col cols="12" sm="12" md="3" xl="2" v-for="(data,index) in agents" :key="index">
                        <v-card class="pb-5 rounded-xl" flat>
                            <v-img :src="data.agent_pic" contain height="200"></v-img>
                            <p class="pt-3 text-center px-3 mb-0 font-weight-bold">{{data.agent_name}}</p>
                            <p class="caption mb-1 text-center px-3 font-weight-bold caption">{{data.agent_info.designation}}</p>
                            <div v-for="(item,ind) in data.agent_info.phone_number" :key="ind" class="text-center">
                                <p class="mb-0 caption blue-grey--text" v-if="item !=''"><v-icon color="indigo" size="20" class="">mdi-phone</v-icon>{{item}}</p>
                            </div>
                        </v-card>
                    </v-col>
                </v-row>
            </v-container>
        </div>
        <div class="px-sm-4 px-lg-15 pt-5">
            <p class="pt-8 text-center display-1 font-weight-light">CONTACT US</p>
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
import BannerImage from '~/components/reuseable/bannerImage'
import ContactUS from '~/components/reuseable/contact-us-form'

export default {
    components: {
        BannerImage,ContactUS
    },
    data(){
        return{
            cards:[
                {icon:'mdi-bullseye-arrow',title:'Mission',desc:'Our mission is to provide Dubai with a real estate agency that listens to client needs along with a loyal customer base, professional team and sterling reputation.'},
                {icon:'mdi-telescope',title:'Vision',desc:'To be the choice for anyone considering buying, selling or renting a property in Dubai and provide service to an outstanding standard, building key relationships.'},
                {icon:'mdi-scale-balance',title:'Values',desc:'We will show integrity, carry out our job with passion, respect one another, show the utmost professionalism and work as a team to meet our clients’ needs.'},
            ],
            agents:[]
        }
    },
    mounted(){
        this.getData()
    },
    methods:{
        async getData(){
            await this.$axios.$get("teams/all")
            .then(res =>{
                this.agents = res
            }).catch()
        },
    },
    computed:{
        
    }
}
</script>