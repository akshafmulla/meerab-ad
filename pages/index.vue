<template>
  <div class="pt-1">
    <Slider />
    <TravelPackage />
    <InvestWithUs />
    <div class="grey lighten-4 pt-5">
      <OffplanSlider />
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
import ContactUS from '~/components/reuseable/contact-us-form'
import ContactUSAdress from '~/components/reuseable/contact-us-address'

export default {
    data(){
      return {
      } 
    },
    async asyncData({app, store}){
    },
    components: {
        Slider,
        TravelPackage,
        InvestWithUs,
        Partners,
        OffplanSlider,
        ContactUS,
        ContactUSAdress,
    }
}
</script>