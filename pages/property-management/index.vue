<template>
    <div>
        <BannerImage image_url="https://meerabproperties.s3.ap-south-1.amazonaws.com/Property+Management.jpg" />
        <div class="grey lighten-4">
            <p class="pt-8 text-center display-1 font-weight-light">PROPERTY MANAGEMENT</p>
            <v-container>
                <p class="px-sm-4 px-lg-15">Meerab Properties Management ensures that when it comes to your property investment, you are relieved of all the stress and you can rest easy! Our team takes care of conducting snagging for your new home so you can get it in the best condition. Not only that, but we also ensure that your tenant is accountable for any damages incurred in the duration of the tenancy.</p>
                <br>
            </v-container>
        </div>
        <div>
            <v-container>
                <p class="pt-8 text-center display-1 font-weight-bold amber--text accent-4--text">Rest easy with our team of experienced property managers</p>
                <p class="text-center text-h6 font-weight-bold">Meerab Properties Highly Trained Property Management Team Offers Exceptional Services</p>
                <v-layout column align-center justify-center>
                    <v-row class="pt-5">
                        <v-col cols="12" sm="12" md="6" v-for="(data,index) in pmg" :key="index" :class="index % 2 == 0 ? 'text-right' : 'text-left'" class="px-10">
                            <li class="headline">{{data}}</li>
                        </v-col>
                    </v-row>    
                </v-layout>
            </v-container>
        </div>
        <div class="grey lighten-4">
            <v-container>
                <p class="pt-8 text-center display-1 font-weight-bold amber--text accent-4--text">Why Hire Meerab Properties Management Services?</p>
                <p class="px-sm-4 px-lg-15">We are here to make your life easier as a landlord. Employ our services to kickback, relax and just earn the benefits of your investment. With our experienced team available to you 24/7, you can rest stress-free and live your life without any hassle that comes with being a landlord. Your peace of mind is our priority.</p>
                <v-layout column align-center justify-center>
                    <v-container>
                        <v-row class="pt-5">
                            <v-col cols="12" sm="12" md="6" v-for="(data,index) in pmg1" :key="index" class="py-2 px-10">
                                <li class="headline grey--text text--darken-2">{{data}}</li>
                            </v-col>
                        </v-row>  
                    </v-container>
                </v-layout>
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
            pmg:['Snagging Services','Facilities Management','Interior Designing','Building Management','Home Renovation','Additional Services'],
            pmg1:['Peace of Mind','Simple Fixed No-Fuss Annual Fee','Trusted and Experienced Professionals','Earn Maximum Returns','Manage Real Estate Assets in Dubai for local and international clients over a decade','Ensuring Long Term Savings','Always Available for tenants and landlords','Maintain good relations between tenants & landlords']
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