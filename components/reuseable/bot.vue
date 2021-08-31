<template>
<v-container fluid>
  <div class="">
    <v-speed-dial class="mr-n3" v-model="fab1" dark color="green" small fixed right bottom direction="top">
      <template v-slot:activator>
          <v-btn v-model="fab1" color="green" fab dark small >
              <v-icon v-if="fab1"> mdi-close </v-icon>
              <v-icon v-else> mdi-chat </v-icon>
          </v-btn>
      </template>
      <v-tooltip left color="green">
        <template v-slot:activator="{ on, attrs }">
          <v-btn class="" color='white' @click="whatasppRoute"  fab dark small v-bind="attrs" v-on="on">
            <v-icon color="green" size="25">mdi-whatsapp</v-icon>
          </v-btn>
        </template>
      Whatsapp
      </v-tooltip>
      <v-tooltip left color="blue">
        <template v-slot:activator="{ on, attrs }">
          <v-btn class="" color='white'  fab dark small v-bind="attrs" v-on="on">
            <a href="tel:+971565989824" style="text-decoration: none !important;"><v-icon color="blue" size="25">mdi-phone</v-icon></a> 
          </v-btn>
        </template>
      Calling
      </v-tooltip>
    </v-speed-dial>
    <!-- <v-speed-dial class="mr-n3" v-model="fab" dark color="blue" small fixed right bottom direction="top" style="margin-bottom : 50px; !important">
      <template v-slot:activator>
          <v-btn v-model="fab" color="blue" fab dark small >
              <v-icon v-if="fab"> mdi-close </v-icon>
              <v-icon v-else> mdi-robot </v-icon>
          </v-btn>
      </template>
      <v-tooltip left color="pink">
        <template v-slot:activator="{ on, attrs }">
          <v-btn class="" color='white'  fab dark small v-bind="attrs" v-on="on">
            <a href="https://www.instagram.com/meerabproperties/" style="text-decoration: none !important;"><v-icon color="pink" size="25">mdi-instagram</v-icon></a> 
          </v-btn>
        </template>
      Instagram
      </v-tooltip>
      <v-tooltip left color="blue">
        <template v-slot:activator="{ on, attrs }">
          <v-btn class="" color='white'  fab dark small v-bind="attrs" v-on="on">
            <a href="https://www.facebook.com/profile.php?id=100072154745739" style="text-decoration: none !important;"><v-icon color="blue" size="25">mdi-facebook</v-icon></a> 
          </v-btn>
        </template>
      Facebook
      </v-tooltip>
      <v-tooltip left color="blue">
        <template v-slot:activator="{ on, attrs }">
          <v-btn class="" color='white'  fab dark small v-bind="attrs" v-on="on">
            <a href="https://www.linkedin.com/in/meerab-properties" style="text-decoration: none !important;"><v-icon color="blue" size="25">mdi-linkedin</v-icon></a> 
          </v-btn>
        </template>
      LinkedIn
      </v-tooltip>
      <v-tooltip left color="cyan">
        <template v-slot:activator="{ on, attrs }">
          <v-btn class="" color='white'  fab dark small v-bind="attrs" v-on="on">
            <a href="https://twitter.com/MeerabProperty" style="text-decoration: none !important;"><v-icon color="cyan" size="25">mdi-twitter</v-icon></a> 
          </v-btn>
        </template>
      Twitter
      </v-tooltip>
    </v-speed-dial> -->
    
    <!-- <v-menu class="mr-5" min-width = "300" max-width="500" top v-model="menu" :close-on-click="false" :close-on-content-click="false" :nudge-top="30" offset-x>
      <template v-slot:activator="{ on }">
        <v-fab-transition>
          <v-btn small v-model="fab" v-on="on" color='white' @click="fab = !fab; menu = false" dark fixed bottom right fab>
            <v-icon color="green">mdi-whatsapp</v-icon>
          </v-btn>
        </v-fab-transition>
      </template>
      <v-card class="rounded-xl">
        <v-list dark class="chat-header">
          <v-list-item>
            <v-list-item-content>
              <v-list-item-title class="subtitle-1 pl-3">Welcome To Meerab Properties customer support!</v-list-item-title><br>
              <p class="caption pl-3">We are Dubai based properties consultants for latest projects.</p>
            </v-list-item-content>
            <v-list-item-action>
              <v-btn icon @click="fab = !fab; menu = false">
                <v-icon class="align--end">mdi-close</v-icon>
              </v-btn>
            </v-list-item-action>
          </v-list-item>
        </v-list>
        <v-divider></v-divider>
        <v-container class="chat-background">
          <v-layout row wrap >
            <v-flex class="text-xs-right pl-4 justify-end" xs12 mb-4>
              <v-chip class="chip-chat">
                Hello! I am your assistant, how can I help you? <v-icon right>mdi-done_all</v-icon>
              </v-chip>
            </v-flex>
            <v-flex xs10>
              <v-text-field outlined dense single-line placeholder="Enter Message Here!!" class="teal--text my-input ml-4" v-model="text" outline></v-text-field>
            </v-flex>
            <v-flex xs2>
              <v-btn large class="black--text" icon @click="fab = !fab; menu = false" :href="apilink" target="_blank">
                <v-icon>mdi-send</v-icon>
              </v-btn>
              </v-flex>
            </v-layout>  
        </v-container>
      </v-card>  
    </v-menu> 
    <v-btn style="margin-bottom : 50px; !important" small color='white'  dark fixed bottom right fab>
      <a href="tel:+971504243914" style="text-decoration: none !important;"><v-icon color="blue" size="20">mdi-phone</v-icon></a> 
    </v-btn>  -->
    </div>
  </v-container>
  
</template>
  
<script>

// import 'vue-whatsapp-widget'
  export default {
    // components:{VueWhatsappWidget},
    data: () => ({
        fab: false,
        fab1: false,
        fab2: false,
        fav: true,
        menu: false,
        message: false,
        hints: true,
        phone: '971565989824',
        text: "",
        apilink: "",
        isEmailSent: false,
        form: {
            email: ''
        },
        isAuth: true,
        tabs: null,
        loginDialog: false,
    }),
    created: function () {
      this.apilink = 'https://wa.me/' + this.phone + '?text=' + encodeURI("Hello!");
    },
    mounted(){
       
    },
    methods: {
      whatasppRoute(){
        window.open('https://wa.me/'+ this.phone + '?text=' + encodeURI("Hello!"), '_blank')
      },
        closeDialog: function(){
            this.loginDialog = false
            if(this.$store.getters.isAuthenticated){
                this.getaddresses()
            }
        },
        isMobile() {
          var check = false;
          (function(a){if(/(android|bb\d+|meego).+mobile|avantgo|bada\/|blackberry|blazer|compal|elaine|fennec|hiptop|iemobile|ip(hone|od)|iris|kindle|lge |maemo|midp|mmp|mobile.+firefox|netfront|opera m(ob|in)i|palm( os)?|phone|p(ixi|re)\/|plucker|pocket|psp|series(4|6)0|symbian|treo|up\.(browser|link)|vodafone|wap|windows ce|xda|xiino/i.test(a)||/1207|6310|6590|3gso|4thp|50[1-6]i|770s|802s|a wa|abac|ac(er|oo|s\-)|ai(ko|rn)|al(av|ca|co)|amoi|an(ex|ny|yw)|aptu|ar(ch|go)|as(te|us)|attw|au(di|\-m|r |s )|avan|be(ck|ll|nq)|bi(lb|rd)|bl(ac|az)|br(e|v)w|bumb|bw\-(n|u)|c55\/|capi|ccwa|cdm\-|cell|chtm|cldc|cmd\-|co(mp|nd)|craw|da(it|ll|ng)|dbte|dc\-s|devi|dica|dmob|do(c|p)o|ds(12|\-d)|el(49|ai)|em(l2|ul)|er(ic|k0)|esl8|ez([4-7]0|os|wa|ze)|fetc|fly(\-|_)|g1 u|g560|gene|gf\-5|g\-mo|go(\.w|od)|gr(ad|un)|haie|hcit|hd\-(m|p|t)|hei\-|hi(pt|ta)|hp( i|ip)|hs\-c|ht(c(\-| |_|a|g|p|s|t)|tp)|hu(aw|tc)|i\-(20|go|ma)|i230|iac( |\-|\/)|ibro|idea|ig01|ikom|im1k|inno|ipaq|iris|ja(t|v)a|jbro|jemu|jigs|kddi|keji|kgt( |\/)|klon|kpt |kwc\-|kyo(c|k)|le(no|xi)|lg( g|\/(k|l|u)|50|54|\-[a-w])|libw|lynx|m1\-w|m3ga|m50\/|ma(te|ui|xo)|mc(01|21|ca)|m\-cr|me(rc|ri)|mi(o8|oa|ts)|mmef|mo(01|02|bi|de|do|t(\-| |o|v)|zz)|mt(50|p1|v )|mwbp|mywa|n10[0-2]|n20[2-3]|n30(0|2)|n50(0|2|5)|n7(0(0|1)|10)|ne((c|m)\-|on|tf|wf|wg|wt)|nok(6|i)|nzph|o2im|op(ti|wv)|oran|owg1|p800|pan(a|d|t)|pdxg|pg(13|\-([1-8]|c))|phil|pire|pl(ay|uc)|pn\-2|po(ck|rt|se)|prox|psio|pt\-g|qa\-a|qc(07|12|21|32|60|\-[2-7]|i\-)|qtek|r380|r600|raks|rim9|ro(ve|zo)|s55\/|sa(ge|ma|mm|ms|ny|va)|sc(01|h\-|oo|p\-)|sdk\/|se(c(\-|0|1)|47|mc|nd|ri)|sgh\-|shar|sie(\-|m)|sk\-0|sl(45|id)|sm(al|ar|b3|it|t5)|so(ft|ny)|sp(01|h\-|v\-|v )|sy(01|mb)|t2(18|50)|t6(00|10|18)|ta(gt|lk)|tcl\-|tdg\-|tel(i|m)|tim\-|t\-mo|to(pl|sh)|ts(70|m\-|m3|m5)|tx\-9|up(\.b|g1|si)|utst|v400|v750|veri|vi(rg|te)|vk(40|5[0-3]|\-v)|vm40|voda|vulc|vx(52|53|60|61|70|80|81|83|85|98)|w3c(\-| )|webc|whit|wi(g |nc|nw)|wmlb|wonu|x700|yas\-|your|zeto|zte\-/i.test(a.substr(0,4))) check = true;});
          return check;
        },
    },
    
  }
</script>

<style >
.my-input.v-input .v-input__slot {
    border-radius: 100px;
}

.chat-background {
    background-color: #ffffff !important
}

.chat-header {
    background-color: #0c5020 !important
}

.chip-chat {
    background-color: #EEEEEE !important
}

.wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>