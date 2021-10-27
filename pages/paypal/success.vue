<template>
    <div class="pa-5">
        <!-- {{returnValue}} -->
        <v-layout column align-center justify-center >
            <v-img src="/paypal.png" max-height="150"></v-img>
            <p class="text-h4 font-weight-bold pt-5 primary--text">Congratulations</p>
            <p class="text-h5 font-weight-light pt-2 black--text">Your transaction was successful.&nbsp;<v-icon class="mt-n2" size="30" color="green">mdi-check-circle</v-icon></p>
            <p class="text-h6 font-weight-light black--text">Below is your transaction ID.</p>
            <p class="text-h5 font-weight-bold black--text">{{returnValue.paymentId}}</p>
            <p>
                <v-btn class="purple white--text mr-3" @click="email_dialog = true"><v-icon>mdi-email</v-icon>&nbsp;send email</v-btn>
                <v-btn class="primary white--text" to="/"><v-icon>mdi-home</v-icon>&nbsp;Home</v-btn>
            </p>
        </v-layout>

        <!-- Send Email Dialog -->
        <v-dialog v-model="email_dialog" max-width="400">
            <v-card color="white" style="overflow-x:hidden;" dark class="pa-3">
                <v-card-title class="primary--text">
                    Send Payment ID on Email
                </v-card-title>
                <v-card-text class="mb-0">
                    <v-form ref="form">
                        <p class="mb-0 primary--text font-weight-bold caption">Enter Email ID</p>
                        <v-text-field type="email" placeholder="Enter Email ID" solo dense prepend-inner-icon="mdi-email" v-model="emailId" :rules="emailRules"></v-text-field>
                    </v-form>
                </v-card-text>
                <p class="mb-0 mt-n5 text-right"><v-btn class="primary--text" text small @click="sendEmail">Send Email</v-btn></p>
            </v-card>
        </v-dialog>

        <!-- Snackbar -->
        <v-snackbar v-model="snack" :timeout="3000" :color="snackColor">
            {{ snackText }}
            <template v-slot:action="{ attrs }">
                <v-btn v-bind="attrs" text @click="snack = false">Close</v-btn>
            </template>
        </v-snackbar>
    </div>
</template>

<script>
export default {
    data(){
        return{
            returnValue : {},
            email_dialog:false,
            emailId:'',
            snack:false,
            snackColor:'',
            snackText:'',
            emailRules: [ 
                v => !v || /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid'
            ]
        }
    },
    mounted(){
        this.returnValue = this.$route.query
        // this.successEmail()
    },
    methods:{
        sendEmail(){
            if(this.$refs.form.validate()){
                let emailBody={
                    hr_email : 'payments@meerabproperties.com',
                    email:this.emailId,
                    subject:'Paypal Payment Reference ID',
                    eMessage:'Hey,<br/><br/>As requested, PFB payment ID for the transaction details:<br/><br/>Payment ID : <b>'+ this.returnValue.paymentId+'</b><br/>Please use this transaction ID for future interaction about the property.<br/><br/>Thank You for your time. Have a great day ahead.<br/><br/>Regards,<br/>Meerab Properties'
                }
                this.$axios.$post('properties/send-email/', emailBody).then(res=>{
                    this.snack = true
                    this.snackText = 'Details have been sent! Please check your inbox!'
                    this.snackColor = "primary"
                    this.$refs.form.reset()
                    this.email_dialog = false
                }).catch(e => console.log(e))
            }
        },
        successEmail(){
            let emailBody={
                hr_email: 'payments@meerabproperties.com',
                email: ['vinay.sharma1708@gmail.com','akshafmulla@gmail.com'],
                // email: ['vinay.sharma1708@gmail.com','shaikh@meerabproperties.com'],
                subjectMsg: 'New Payment Received - Paypal',
                eMessage: 'Hey,<br/><br/>A new Payment has been received on www.meerabproperties.com. PFB payment ID for the transaction details:<br/><br/>Payment ID : <b>'+ this.returnValue.paymentId+'</b><br/><br/>Thank You for your time. Have a great day ahead.<br/><br/>Regards,<br/>Meerab Properties'
            }
            this.$axios.$post('properties/send-email/', emailBody).then(res=>{}).catch(e => console.log(e))
        }
    },
    computed:{
        windowSize(){
            return this.$vuetify.breakpoint.mobile ? true : false
        },
    }
}
</script>