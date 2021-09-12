<template>
    <div>
        <v-img :src="property.banner_img" cover height="500"></v-img>
        <v-container v-if="property">
            <p class="pt-5 text-center primary--text text-h4 mb-4">{{property.property_name}}</p>
            <p class="mb-0 text-center"><v-chip class="indigo white--text" x-small>{{property.property_type}}</v-chip></p>
            <p class="mb-1  text-center">{{property.community}} by {{property.developer}}</p>
            <p class=" text-center"><v-icon class="mt-n1" color="primary" size="15">mdi-warehouse</v-icon>&nbsp;<span v-for="(item, i) in property.rooms" :key="i">{{item}}<span v-if="i < property.rooms.length - 1">,&nbsp;</span> </span> Rooms&emsp;&emsp;<v-icon color="green" size="15" class="mt-n1">mdi-cash</v-icon>&nbsp;Starting {{property.starting_price | amountFormatter}} AED</p>
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
                <v-row justify="center" align="center">
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
            // projects: [
            //     {property_details:{},property_pics:['https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/0.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/1.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/2.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/3.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/4.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/5.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/6.JPG'],location:'Creek Harbour',property_type:'Building',builder_name:'Emaar',rooms:[3,4],banner_img:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/Banner.jpg',property_name:'Creek Horizon at Dubai Creek Harbour'},

            //     {property_details:{},property_pics:['https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Caya/1.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Caya/2.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Caya/3.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Caya/4.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Caya/5.JPG'],location:'Arabian Ranches 3',property_type:'Building',builder_name:'Emaar',rooms:[3,4],banner_img:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Caya/Banner.JPG',property_name:'Caya at Arabian Ranches 3 by Emaar'},

            //     {property_details:{},property_pics:['https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Aseel/2.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Aseel/3.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Aseel/4.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Aseel/5.JPG'],location:'Arabian Ranches',property_type:'Building',builder_name:'Emaar',rooms:[3,4],banner_img:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Aseel/Banner.JPG',property_name:'Aseel at Arabian Ranches by Emaar'},

            //     {property_details:{},property_pics:[],location:'Downtown Dubai',property_type:'Building',builder_name:'Emaar',rooms:[3,4],banner_img:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Opera+Grand/Banner.JPG',property_name:'Opera Grand at Downtown Dubai by Emaar'},
            //     {property_details:{},property_pics:[],location:'Creek Harbour',property_type:'Building',builder_name:'Emaar',rooms:[3,4],banner_img:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/Banner.jpg',property_name:'Creek Horizon at Dubai Creek Harbour by Emaar'},
            //     {property_details:{},property_pics:[],location:'Creek Harbour',property_type:'Building',builder_name:'Emaar',rooms:[3,4],banner_img:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Harbour+Gate/Banner.jpg',property_name:'Harbour Gate at Dubai Creek Harbour by Emaar'},
            //     {property_details:{},property_pics:[],location:'Dubai Hills Estate',property_type:'Building',builder_name:'Emaar',rooms:[3,4],banner_img:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Mulberry/Banner.jpg',property_name:'Mulberry at Dubai Hills Estate by Emaar'},
            // ],
            property:{
                property_name:'',
                location:'',
                property_type:'',
                builder_name:'',
                rooms:[],
                banner_img:'',
                property_details:{},
                property_pics:[]
            },
            dialog_image:''
        }
    },
    mounted(){
        this.onload()
    },
    methods:{
        async onload(){
            await this.$axios.$get('properties/'+this.$route.params.id.replace(/-/g,' '))
            .then(res=>{
                console.log(res)
                this.property = res[0]
            })
            .catch(e => console.log(e))
        },
        // propertyDetails(){
        //     let abc = this.$route.params.id.replace(/-/g,' ')
        //     let d = this.projects.filter(a => a.property_name == abc)
        //     d.length > 0 ? this.property = d[0] : {}
        // },
        loadImg(index){
            this.dialog_image = this.property.property_pics[index].link
            this.dialog = true
        }
    },
    computed:{
        createCarousal(){

        }
    }
}
</script>