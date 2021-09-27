<template>
    <div>
        <v-btn @click="paypal">buy</v-btn>
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
        paypal(){
            this.$axios.post('/paypal/pay',{})
            .then(res =>{
                console.log(res)
            }).catch()
        }
    },
    computed:{
        
    }
}
</script>