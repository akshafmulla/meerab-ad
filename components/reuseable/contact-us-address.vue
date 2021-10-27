<template>
    <div class="text-left">
        <v-card class="rounded-xl pa-5" flat>
            
            <!-- <p class="caption mb-3 font-weight-bold"><v-img contain height="10" src="https://meerabproperties.s3.ap-south-1.amazonaws.com/Static/uae-flag.png">&emsp;03, 1st Floor, F1RST MOTORS, DUBAI, UAE</v-img></p> -->
            <!-- <div style="display : flex;">
                <v-img contain height="10" src="https://meerabproperties.s3.ap-south-1.amazonaws.com/Static/uae-flag.png" /> &emsp;03, 1st Floor, F1RST MOTORS, DUBAI, UAE
            </div> -->
            <v-row>
                <v-col cols="1" sm="1" class="text-right my-auto pt-0 px-0 ml-xl-n2">
                    <v-img contain height="10" src="https://meerabproperties.s3.ap-south-1.amazonaws.com/Static/uae-flag.png" />
                </v-col>
                <v-col cols="11" sm="11" class="ml-xl-n2 py-0 px-md-0">
                    <p class="caption mb-3 font-weight-bold">03, 1st Floor, F1RST MOTORS, DUBAI, UAE</p>
                </v-col>
                <v-col cols="1" sm="1" class="text-right my-auto pt-0 px-0 ml-xl-n2">
                    <v-img contain height="10" src="https://meerabproperties.s3.ap-south-1.amazonaws.com/Static/us-flag.png" />
                </v-col>
                <v-col cols="11" sm="11" class="ml-xl-n2 py-0 px-md-0">
                    <p class="caption mb-3 font-weight-bold">924 US ROUTE 9, SUITE 200 SOUTH AMBOY, NEW JERSEY 08879, US</p>
                </v-col>
            </v-row>
            <p class="mb-3 caption font-weight-bold"><v-icon size="20" class="mt-n1" color="#af880a">mdi-phone</v-icon>&emsp;&emsp;+971 569180786</p>
            <p class="mb-3 caption font-weight-bold"><v-icon size="20" class="mt-n1" color="#af880a">mdi-email-outline</v-icon>&emsp;&emsp;info@meerabproperties.ae</p>
            <p class="mb-3 caption font-weight-bold"><v-icon size="20" class="mt-n1" color="#af880a">mdi-calendar-clock-outline</v-icon>&emsp;&emsp;Saturday – Thursday 9:00 : 18:00 UAE </p>   
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
                eMessage: 'Hey,<br/><br/>A new Lead has been received on www.meerabproperties.com.PFB details:<br/><br/>Name : <b>'+ this.contact.first_name+ ' ' + this.contact.last_name+ '</b><br/><br/>Email : <b>'+ this.contact.email+ '</b><br/><br/>Contact No. : <b>'+ this.contact.mobile+'</b><br/><br/>Address : <b>'+ this.contact.address+'</b><br/><br/>Thank You for your time. Have a great day ahead.<br/><br/>Regards,<br/>Meerab Properties'
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