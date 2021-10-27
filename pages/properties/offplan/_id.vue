<template>
    <div class="grey lighten-4">
        <v-img :src="property.banner_img" cover height="500"></v-img>
        <v-layout column align-center justify-center :class="windowSize ? '' : ''" >
            <v-card flat color="white" class="white pa-4" :class="windowSize ? '' : 'margin'" >
                <h1 class="primary--text">{{property.property_name}}</h1>
                <p class="mb-5 caption"><v-icon class="mt-n2">mdi-map-marker-radius</v-icon>&nbsp;{{property.community}}</p>
                <v-divider></v-divider>
                <v-row class="font-weight-bold caption">
                    <v-col cols="6" sm="6" class="">
                        <p class="mb-0 primary--text"><v-icon color="primary">mdi-cash</v-icon>&nbsp; Starting Price</p>
                    </v-col>
                    <v-col cols="6" sm="6" class="text-right">
                        <p class="mb-0">AED &nbsp;{{property.starting_price | amountFormatter}}</p>
                    </v-col>
                </v-row>
                <v-divider></v-divider>
                <v-row class="font-weight-bold caption">
                    <v-col cols="6" sm="6" class="">
                        <p class="mb-0 primary--text"><v-icon color="primary">mdi-label-multiple-outline</v-icon>&nbsp; Community</p>
                    </v-col>
                    <v-col cols="6" sm="6" class="text-right">
                        <p class="mb-0">{{property.community}}</p>
                    </v-col>
                </v-row>
                <v-divider></v-divider>
                <v-row class="font-weight-bold caption">
                    <v-col cols="6" sm="6" class="">
                        <p class="mb-0 primary--text"><v-icon color="primary">mdi-bed</v-icon>&nbsp; Bedrooms</p>
                    </v-col>
                    <v-col cols="6" sm="6" class="text-right">
                        <p class="mb-0"><span v-for="(item, i) in property.rooms" :key="i">{{item}}<span v-if="i < property.rooms.length - 1">,&nbsp;</span> </span> Rooms</p>
                    </v-col>
                </v-row>
                <v-divider></v-divider>
                <v-row class="font-weight-bold caption">
                    <v-col cols="6" sm="6" class="">
                        <p class="mb-0 primary--text"><v-icon color="primary">mdi-warehouse</v-icon>&nbsp; Type</p>
                    </v-col>
                    <v-col cols="6" sm="6" class="text-right">
                        <p class="mb-0">{{property.property_type}}</p>
                    </v-col>
                </v-row>
                <v-divider></v-divider>
                <v-row class="font-weight-bold caption">
                    <v-col cols="6" sm="6" class="">
                        <p class="mb-0 primary--text"><v-icon color="primary">mdi-chart-areaspline-variant</v-icon>&nbsp; Area</p>
                    </v-col>
                    <v-col cols="6" sm="6" class="text-right">
                        <p class="mb-0">{{property.area[0]}} - {{property.area[1]}} Sq. Ft</p>
                    </v-col>
                </v-row>
                <v-row class="font-weight-bold caption">
                    <v-col cols="6" sm="5" class="text-center">
                        <v-btn class="indigo" @click="paypal()" depressed :disabled="true">Book Now</v-btn>
                    </v-col>
                    <v-col cols="6" sm="7" class="text-left">
                        <v-btn class="primary" dark href="#contact-us">Register Interest</v-btn>
                    </v-col>
                </v-row>
            </v-card>
        </v-layout>
        <v-container v-if="property" class="white mt-4">
            <h4 class="pl-3 blue-grey--text">Overview</h4>
            <v-row class="pl-3 " v-for="(data,index) in property.overview" :key="index">
                <v-col cols="12" sm="12" md="12" class="pb-0">    
                    <p class="mb-0" v-if="data.type == 'text'">{{data.text}}</p>
                    <v-container v-else>
                        <v-row>
                            <v-col class="py-0" cols="12" sm="12" md="6" v-for="(item,ind) in data.text" :key="ind">
                                <ul>
                                    <li>{{item.val}}</li>
                                </ul>
                            </v-col>
                        </v-row>
                    </v-container>
                </v-col>
            </v-row>
            <h4 class="py-4 pl-3 blue-grey--text">Property Pictures</h4>
            <v-row class="pl-3">
                <v-col cols="12" sm="12" md="3" xl="2"  v-for="(data,index) in property.property_pics" :key="index">
                    <v-img :src="data.link" height="150" width="250" @click="loadImg(index)"/>
                </v-col>
            </v-row>
            <h4 class="pt-3 pl-3 blue-grey--text">Location</h4>
            <v-row class="pl-3 " v-for="(data,index) in property.location" :key="index">
                <v-col cols="12" sm="12" md="12" class="pb-0">    
                    <p class="mb-0" v-if="data.type == 'text'">{{data.text}}</p>
                    <v-container v-else>
                        <v-row>
                            <v-col class="py-0" cols="12" sm="12" md="6" v-for="(item,ind) in data.text" :key="ind">
                                <ul>
                                    <li>{{item.val}}</li>
                                </ul>
                            </v-col>
                        </v-row>
                    </v-container>
                </v-col>
            </v-row>
            <h4 class="pt-3 pl-3 blue-grey--text">Ammenities</h4>
            <v-container>
                <v-row class="pl-3 ">
                    <v-col cols="12" sm="12" md="3" class="pt-0 pb-1"  v-for="(data,index) in property.ammenities" :key="index">    
                        <ul>
                            <li>{{data}}</li>
                        </ul>
                    </v-col>
                </v-row>
            </v-container>
            <p class="pt-5 text-center display-1 font-weight-light">CONTACT US</p>
            <v-layout column align-center justify-center>
                <v-row justify="center" align="center" id="contact-us">
                    <v-col cols="12" sm="12" >
                        <ContactUS />
                    </v-col>
                </v-row>
            </v-layout>
        </v-container>
        <!-- image dialog -->
        <v-dialog v-model="dialog" color="rgb(255, 0, 0, 1)" overlay-opacity="100" max-width="900px">
            <v-card class="" style="overflow-x : hidden">
                <v-img :src="dialog_image" max-height="550" cover></v-img>
            </v-card>
        </v-dialog>
    </div>
</template>

<script>
import ContactUS from '~/components/reuseable/contact-us-form'

export default {
    components: {ContactUS},
    data(){
        return{
            dialog:false,
            property:{
                property_name:'',
                location:'',
                property_type:'',
                builder_name:'',
                rooms:[],
                banner_img:'',
                property_details:{},
                property_pics:[],
                area:[]
            },
            dialog_image:'',
        }
    },
    mounted(){
        this.onload()
    },
    methods:{
        paypal(){
            let paypal_property_name = this.$route.params.id
            this.$axios.post('/paypal/pay', {property_name : paypal_property_name})
            .then(res =>{
                console.log(res)
                if(res.data != '') window.open(res.data)
            }).catch()
        },
        async onload(){
            await this.$axios.$get('properties/'+this.$route.params.id.replace(/-/g,' '))
            .then(res=>{
                this.property = res[0]
            })
            .catch(e => console.log(e))
        },
        loadImg(index){
            this.dialog_image = this.property.property_pics[index].link
            this.dialog = true
        }
    },
    computed:{
        windowSize(){
            return this.$vuetify.breakpoint.mobile ? true : false
        },
        
    }
}
</script>

<style>
.margin{
    margin-top : -280px;
}
</style>