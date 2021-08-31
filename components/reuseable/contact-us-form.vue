<template>
    <div class="px-5">
        <v-card class="rounded-xl pa-5" flat max-width="900" min-height="390">
            <p class="body-1 mb-5 font-weight-bold text-center" style="color : #af880a;">Enter the below details. We will reach out to you soon!!</p>
            <v-form v-model="valid" ref="form">
                <v-row >
                    <v-col class="py-0" cols="12" sm="12" md="6">
                        <p class="caption font-weight-bold mb-0">First Name</p>
                        <v-text-field dense outlined v-model="contact.first_name" placeholder="First Name" :rules="genericRule"></v-text-field>
                    </v-col>
                    <v-col  class="py-0" cols="12" sm="12" md="6">
                        <p class="caption font-weight-bold mb-0">Last Name</p>
                        <v-text-field dense outlined v-model="contact.last_name" placeholder="Last Name" :rules="genericRule"></v-text-field>
                    </v-col>
                    <v-col  class="py-0" cols="12" sm="12" md="6">
                        <p class="caption font-weight-bold mb-0">Email</p>
                        <v-text-field dense outlined v-model="contact.email" placeholder="Email ID" :rules="genericRule"></v-text-field>
                    </v-col>
                    <v-col  class="py-0" cols="12" sm="12" md="6">
                        <p class="caption font-weight-bold mb-0">Contact Number</p>
                        <v-text-field dense outlined v-model="contact.mobile" type="number" placeholder="Mobile Number" :rules="genericRule"></v-text-field>
                    </v-col>
                    <v-col  class="py-0" cols="12" sm="12" md="12">
                        <!-- <country-select style="border : 1px solid #9a9393; border-radius : 4px;" v-model="country" :country="country" topCountry="AE" /> -->
                        <!-- <region-select style="border : 1px solid #9a9393;  border-radius : 4px;" v-model="region" :country="country"  :region="region" /> -->
                        <p class="caption font-weight-bold mb-0">Location</p>
                        <v-text-field dense outlined v-model="contact.address" placeholder="Address" :rules="genericRule"></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="12" class="pt-0 text-right">
                        <v-btn color="#af880a" dark @click="sendELead">Submit</v-btn>
                    </v-col>
                    <!-- <v-col  class="pb-0" cols="12" sm="12" md="12">
                        <v-text-field dense outlined v-model="contact.region" placeholder="Select Region" :rules="genericRule"></v-text-field>
                    </v-col> -->
                </v-row>
            </v-form>
        </v-card>
        <!-- Snackbar -->
        <v-snackbar
            v-model="snack"
            :timeout="3000"
            :color="snackColor"
            >
            {{ snackText }}
            <template v-slot:action="{ attrs }">
                <v-btn v-bind="attrs" text @click="snack = false">Close</v-btn>
            </template>
        </v-snackbar>
    </div >
</template>

<script>
export default {
    data(){
        return{
            valid:'',
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
            },
            genericRule: [
                v => !!v || 'This field is Required'
            ],
            snack:false,
            snackText:'',
            snackColor:'',
        }
    },
    mounted(){

    },
    methods:{
        sendELead(){
            if(this.$refs.form.validate()){
                let url = 'https://www.meerabproperties.com'.concat(this.$route.path)
                let emailBody = {
                    hr_email: 'leads@meerabproperties.com',
                    email: this.contact.email,
                    subjectMsg: 'New Lead',
                    eMessage: 'Hey,<br/><br/>A new Lead has been received on www.meerabproperties.com.PFB details:<br/><br/>Name : <b>'+ this.contact.first_name+ ' ' + this.contact.last_name+ '</b><br/><br/>Email : <b>'+ this.contact.email+ '</b><br/><br/>Contact No. : <b>'+ this.contact.mobile+'</b><br/><br/>Address : <b>'+ this.contact.address+'</b><br/><br/>Link : <b>'+ url+'</b><br/><br/>Thank You for your time. Have a great day ahead.<br/><br/>Regards,<br/>HR Direct'
                }

                console.log(emailBody)
                this.$axios.$post('properties/send-email/', emailBody).then(res=>{
                    this.snack = true
                    this.snackText = 'Details have been sent! We will reach out to you soon!'
                    this.snackColor = "primary"
                    this.$refs.form.reset()
                }).catch(e => console.log(e))
            }
        }
    },
    computed:{
        
    }
}
</script>