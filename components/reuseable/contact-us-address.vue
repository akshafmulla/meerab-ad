<template>
    <div class="text-left">
        <v-card class="rounded-xl pa-5" flat>
            <p class="caption mb-3 font-weight-bold"><v-icon size="20" class="mt-n1" color="amber accent-4 ">mdi-home</v-icon>&emsp;03, 1st Floor, F1RST MOTORS, DUBAI, UAE</p>
            <p class="mb-3 caption font-weight-bold"><v-icon size="20" class="mt-n1" color="amber accent-4 ">mdi-phone</v-icon>&emsp;+971 0569180786</p>
            <p class="mb-3 caption font-weight-bold"><v-icon size="20" class="mt-n1" color="amber accent-4 ">mdi-phone-classic</v-icon>&emsp;+971 4 2599266</p>
            <p class="mb-3 caption font-weight-bold"><v-icon size="20" class="mt-n1" color="amber accent-4 ">mdi-text-box-outline</v-icon>&emsp;+971 4 2595049</p>
            <p class="mb-3 caption font-weight-bold"><v-icon size="20" class="mt-n1" color="amber accent-4 ">mdi-email-outline</v-icon>&emsp;info@meerabproperties.ae</p>
            <p class="mb-3 caption font-weight-bold"><v-icon size="20" class="mt-n1" color="amber accent-4 ">mdi-calendar-clock-outline</v-icon>&emsp;Saturday – Thursday 9:00 -- 18:00</p>   
        </v-card>
    </div >
</template>

<script>
export default {
    data(){
        return{
            country:'',
            region:'',
            contact:{
                first_name:'',
                last_name:'',
                email:'',
                mobile:'',
                address:'',
                country:'',
                region:''
            }
        }
    },
    mounted(){

    },
    methods:{
        sendELead(){
            let emailBody = {
                hr_email: 'leads@meerabproperties.com',
                email: this.contact.email,
                subjectMsg: 'New Lead',
                eMessage: 'Hey,<br/><br/>A new Lead has been received on www.meerabproperties.com.PFB details:<br/><br/>Name : <b>'+ this.contact.first_name+ ' ' + this.contact.last_name+ '</b><br/><br/>Email : <b>'+ this.contact.email+ '</b><br/><br/>Contact No. : <b>'+ this.contact.mobile+'</b><br/><br/>Address : <b>'+ this.contact.address+'</b><br/><br/>Thank You for your time. Have a great day ahead.<br/><br/>Regards,<br/>HR Direct'
            }

            console.log(emailBody)
            this.$axios.$post('properties/send-email/', emailBody)
            .then(res=>console.log(res)).catch(e => console.log(e))
        }
    },
    computed:{
        
    }
}
</script>