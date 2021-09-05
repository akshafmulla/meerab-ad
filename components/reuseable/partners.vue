<template>
    <div class="mx-15 mt-5">
        <p class="text-center display-1 font-weight-light" style="color : #af880a;">PARTNERS</p>
        <v-row class="px-10" justify="center">
            <v-col cols="12" sm="6" md="4" lg="2" class="text-center" v-for="(data,index) in partners" :key="index"  style="cursor:pointer;">
                <v-card flat class="text-center" :to="data.name == 'Sobha' ? '/partners' : ''"> <!-- :to="`/partners/${data.name}` -->
                    <v-img :src="data.src" max-height="150" max-width="150" :class="index== 0 ? 'mt-n3' : index ==  1 ? 'mt-4' : index == 3 ? 'mt-n2' : index == 4? 'mt-n5' :''"></v-img>
                </v-card>
            </v-col>
        </v-row>
    </div>
</template>

<script>

export default {
    
    data(){
        return{
            partners:[
                {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/builders/damac.png',name:'Damac'},
                {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/builders/emaar.png',name:'Emaar'},
                {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/builders/sobha.png',name:'Sobha'},
                {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/builders/meeras.png',name:'Meeras'},
                {src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/builders/nakheel.png',name:'Nakheel'},
            ],
        }
    },
    mounted(){},
    methods:{
        
    },
    computed:{

    }
}
</script>

<style scoped>
    .travelCard{
        background-image: linear-gradient(to right, rgba(191,155,48,1), rgba(255,255,255,1));
    }
</style>