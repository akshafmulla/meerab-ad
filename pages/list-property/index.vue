<template>
    <div>
        <v-carousel hide-delimiters :show-arrows="false">
            <v-carousel-item v-for="(item,i) in items" :key="i" :src="item.src"  style="cursor : pointer;"></v-carousel-item>
        </v-carousel>
        <v-container>
            <v-row>
                <v-col cols="12" sm="12" md="4">
                    <v-hover v-slot="{ hover }">
                        <v-card class="mx-auto" color="grey lighten-4" max-width="600" min-height="100" >
                            <v-card-text class="mx-0 pa-0">
                                text text
                                <v-expand-transition>
                                    <div  v-if="hover"  class="d-flex transition-fast-in-fast-out orange darken-2 v-card--reveal text-h2 white--text"  style="height: 100%;">
                                        $14.99
                                    </div>
                                </v-expand-transition>
                            </v-card-text>
                        </v-card>
                    </v-hover>
                </v-col>
            </v-row>
        </v-container>
    </div>
</template>

<script>
export default {
    data(){
        return{
            items:[{name:'banner1',src:'https://meerabproperties.s3.ap-south-1.amazonaws.com/List-your-property_v2.jpg'}]
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