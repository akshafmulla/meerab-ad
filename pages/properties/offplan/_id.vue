<template>
    <div>
        <v-img :src="property.banner_img" cover height="500"></v-img>
        <v-container v-if="property">
            <p class="pt-5 text-center amber--text text--accent-4 text-h4 mb-4">{{property.property_name}}</p>
            <p class="pt-10 black--text text-h5 mb-4 text-decoration-underline">Overview</p>
            <p class="">{{property.property_type}} with <span v-for="(item,i) in property.rooms" :key="i">{{item}} </span> in {{property.property_name}}. Emaar collaborated with world-renowned designers to create the interiors of these spacious {{property.property_type}}. There are two different sets to pick from Bloom and Flora.</p>
            <ul class="ml-5">
                <li>5-bedroom {{property.property_type}}</li>
                <!-- <li>First-ever {{property.property_type}} Designed by Elie Saab</li> -->
                <li>Nestled within {{property.location}}</li>
                <li>Starting at AED 10 million</li>
                <li>Overlooking the Dubai Skyline</li>
            </ul>
            <div v-if="property.property_pics.length > 0">
                <p class="pt-10 black--text text-h5 mb-4 text-decoration-underline">Photo Gallery</p>
                <v-row justify="center">
                    <v-col cols="12" sm="12" md="4" lg="3" v-for="(img,index) in property.property_pics" :key="index">
                        <v-img :src="img" max-width="350" max-height="350" @click="loadImg(index)"></v-img>
                    </v-col>
                </v-row>
            </div>
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
        <v-dialog v-model="dialog" max-width="900px">
            <v-card class="" style="overflow-x : hidden">
                <v-img :src="dialog_image"></v-img>
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
            projects: [
                {property_details:{},property_pics:['https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/0.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/1.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/2.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/3.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/4.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/5.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/6.JPG'],location:'Creek Harbour',property_type:'Building',builder_name:'Emaar',rooms:[3,4],banner_img:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/Banner.jpg',property_name:'Creek Horizon at Dubai Creek Harbour'},

                {property_details:{},property_pics:['https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Caya/1.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Caya/2.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Caya/3.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Caya/4.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Caya/5.JPG'],location:'Arabian Ranches 3',property_type:'Building',builder_name:'Emaar',rooms:[3,4],banner_img:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Caya/Banner.JPG',property_name:'Caya at Arabian Ranches 3 by Emaar'},

                {property_details:{},property_pics:['https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Aseel/2.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Aseel/3.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Aseel/4.JPG','https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Aseel/5.JPG'],location:'Arabian Ranches',property_type:'Building',builder_name:'Emaar',rooms:[3,4],banner_img:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Aseel/Banner.JPG',property_name:'Aseel at Arabian Ranches by Emaar'},

                {property_details:{},property_pics:[],location:'Downtown Dubai',property_type:'Building',builder_name:'Emaar',rooms:[3,4],banner_img:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Opera+Grand/Banner.JPG',property_name:'Opera Grand at Downtown Dubai by Emaar'},
                {property_details:{},property_pics:[],location:'Creek Harbour',property_type:'Building',builder_name:'Emaar',rooms:[3,4],banner_img:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Creek+Horizon/Banner.jpg',property_name:'Creek Horizon at Dubai Creek Harbour by Emaar'},
                {property_details:{},property_pics:[],location:'Creek Harbour',property_type:'Building',builder_name:'Emaar',rooms:[3,4],banner_img:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Harbour+Gate/Banner.jpg',property_name:'Harbour Gate at Dubai Creek Harbour by Emaar'},
                {property_details:{},property_pics:[],location:'Dubai Hills Estate',property_type:'Building',builder_name:'Emaar',rooms:[3,4],banner_img:'https://meerabproperties.s3.ap-south-1.amazonaws.com/properties/Mulberry/Banner.jpg',property_name:'Mulberry at Dubai Hills Estate by Emaar'},
            ],
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
        this.propertyDetails()
    },
    methods:{
        propertyDetails(){
            let abc = this.$route.params.id.replace(/-/g,' ')
            let d = this.projects.filter(a => a.property_name == abc)
            d.length > 0 ? this.property = d[0] : {}
        },
        loadImg(index){
            this.dialog_image = this.property.property_pics[index]
            this.dialog = true
        }
    },
    computed:{
        createCarousal(){

        }
    }
}
</script>