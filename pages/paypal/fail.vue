<template>
    <div class="pa-5">
        <!-- {{returnValue}} -->
        <v-layout column align-center justify-center >
            <v-img src="/error.jpg" max-height="350" contain></v-img>
            <p class="text-h4 font-weight-bold pt-5 primary--text">SOMETHING WENT WRONG</p>
            <p class="text-h5 font-weight-light pt-2 black--text">Your transaction was UNSUCCESSFUL.&nbsp;<v-icon class="mt-n2" size="30" color="red">mdi-close-circle</v-icon></p>
            <p>
                <v-btn class="primary white--text" to="/"><v-icon>mdi-home</v-icon>&nbsp;Home</v-btn>
            </p>
        </v-layout>
    </div>
</template>

<script>
export default {
    data(){
        return{
            
        }
    },
    mounted(){
    },
    methods:{
        
    },
    computed:{
        windowSize(){
            return this.$vuetify.breakpoint.mobile ? true : false
        },
    }
}
</script>