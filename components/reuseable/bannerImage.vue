<template>
    <div>
        <v-img :src="image_url" cover :gradient="gradiantFlag ? 'to top right, rgba(100,115,201,.33), rgba(25,32,72,.7)' : ''">
             <v-row align="end" v-if="textFlag">
                <!-- <v-col cols="6" sm="6" md="6" class="pt-0"></v-col> -->
                <v-col cols="6" sm="6" md="6" class="align-end pt-0">
                    <v-card class="rounded-xl pl-3 py-2 pt-0 white--text" flat color="transparent">
                        <v-row class="px-3 mx-auto">
                            <v-col cols="12" sm="12" lg="12" class="pb-0 pt-1 text-right ">
                                <h3 class="display-1 white--text">Sobha Realty</h3>
                            </v-col>
                        </v-row>
                    </v-card>
                </v-col>
            </v-row>
            <!-- <v-row align="end">
                <v-col class="align-end">
                    <p class="display-3 ml-5 mb-0 " style="font-family: Open Sans Light;">{{date | time}}</p>
                    <p class="ml-7 mb-0" style="font-family: Open Sans Light; font-size: 20px;">{{date | ticketingDateFormatter}}</p>
                    <h3 class="ml-7" style="font-family: Open Sans Light; font-size: 25px;" v-if="computeEventForTheDay != ''">{{computeEventForTheDay[0].event_text}}</h3>
                </v-col>
            </v-row> -->
        </v-img>
    </div>
</template>

<script>
export default {
    props:['image_url','gradiantFlag','textFlag'],
    data(){
        return{

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