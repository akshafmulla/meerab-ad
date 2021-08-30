<template>
    <div>
        <BannerImage image_url="https://meerabproperties.s3.ap-south-1.amazonaws.com/vip_package/List+property+with+us.jpg" />
        <div class="grey lighten-4">
            <p class="pt-8 text-center display-1 font-weight-light">LIST WITH US</p>
            <p class="text-center headline font-weight-light amber--text text--accent-4">We will Sell/Rent your property with <b>NO RISKS</b></p>
            <!-- & WE WILL SEL/RENT YOUR PROPERTY WITH NO RISKS -->
            <v-container>
                <p class="px-sm-4 px-lg-15">Established in 2013, we are a consultancy that prides ourselves in providing hassle-free tailored real estate advice and consultancy for investors and families alike who are looking to find the perfect home. We strive to offer five-star service in each and every step of the process</p>
                <br>
                <p class="px-sm-4 px-lg-15">We have been working relentlessly to make the process of owning / selling / renting a property hassle-free for investors and end-users alike. Today, we not only help you buy property off plan or ready, but also find the right mortgage financing options, manage your property as well as help you get tenants for a holiday home.</p>
                <br>
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