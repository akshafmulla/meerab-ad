<template>
  <div class="">
    <Slider :configuration="configuration" />
    <TravelPackage />
    <div class="grey lighten-4 pt-5">
      <p class="text-center display-1 font-weight-light">OFFPLAN PROPERTIES</p>
      <OffplanSlider />
    </div>
    <InvestWithUs />
    <div class="grey lighten-4 pt-5">
      <p class="text-center display-1 font-weight-light">FEATURED COMMUNITIES</p>
      <CommunitySlider />
    </div>
    <Partners />
    <div class="grey lighten-4 pt-5">
      <p class="text-center display-1 font-weight-light" >CONTACT US</p>
      <v-layout column align-center justify-center>
        <v-row>
          <v-col cols="12" sm="12" md="6">
            <ContactUS />
          </v-col>
          <v-col cols="12" sm="12" md="6">
            <ContactUSAdress />
          </v-col>
        </v-row>
      </v-layout>
    </div>
  </div>
</template>

<script>
import Slider from '~/components/reuseable/slider'
import TravelPackage from '~/components/reuseable/travel_package'
import InvestWithUs from '~/components/reuseable/invest_with_us'
import Partners from '~/components/reuseable/partners'
import OffplanSlider from '~/components/reuseable/offplan_home_slider'
import CommunitySlider from '~/components/reuseable/community_home_slider'
import ContactUS from '~/components/reuseable/contact-us-form'
import ContactUSAdress from '~/components/reuseable/contact-us-address'

export default {
    data(){
      return {
        configuration:[
          // {
          //   neighbourhoodList:[],
          //   ammenitiesList:[],
          //   developerList:[]
          // }
        ]
      } 
    },
    async asyncData({app, store}){
    },
    mounted(){
      this.getData()
    },
    methods:{
      async getData(){
        await this.$axios.$get("configurations/all")
        .then(res =>{
          this.configuration = res
          console.log(res)
        }).catch()
      },
    },
    components: {
      Slider,
      TravelPackage,
      InvestWithUs,
      Partners,
      OffplanSlider,
      CommunitySlider,
      ContactUS,
      ContactUSAdress,
    }
}
</script>