<template>
    <div class="black">
        <v-container>
            <v-row>
                <v-col cols="12" sm="12" md="6" class="my-auto">
                    <p class="caption grey--text darken-2 mb-0 ">Copyright ©{{new Date().getFullYear()}} Meerab Properties . All Rights Reserved.</p>
                </v-col>
                <v-col cols="12" sm="12" md="6" class="text-md-right" >
                    <v-tooltip top color="pink">
                        <template v-slot:activator="{ on, attrs }">
                        <v-btn class="" color='black'  fab dark small v-bind="attrs" v-on="on">
                            <a href="https://www.instagram.com/meerabproperties/" style="text-decoration: none !important;"><v-icon color="pink" size="25">mdi-instagram</v-icon></a> 
                        </v-btn>
                        </template>
                    Instagram
                    </v-tooltip>
                    <v-tooltip top color="blue">
                        <template v-slot:activator="{ on, attrs }">
                        <v-btn class="" color='black'  fab dark small v-bind="attrs" v-on="on">
                            <a href="https://www.facebook.com/profile.php?id=100072154745739" style="text-decoration: none !important;"><v-icon color="blue" size="25">mdi-facebook</v-icon></a> 
                        </v-btn>
                        </template>
                    Facebook
                    </v-tooltip>
                    <v-tooltip top color="blue">
                        <template v-slot:activator="{ on, attrs }">
                        <v-btn class="" color='black'  fab dark small v-bind="attrs" v-on="on">
                            <a href="https://www.linkedin.com/in/meerab-properties" style="text-decoration: none !important;"><v-icon color="blue" size="25">mdi-linkedin</v-icon></a> 
                        </v-btn>
                        </template>
                    LinkedIn
                    </v-tooltip>
                    <v-tooltip top color="cyan">
                        <template v-slot:activator="{ on, attrs }">
                        <v-btn class="" color='black'  fab dark small v-bind="attrs" v-on="on">
                            <a href="https://twitter.com/MeerabProperty" style="text-decoration: none !important;"><v-icon color="cyan" size="25">mdi-twitter</v-icon></a> 
                        </v-btn>
                        </template>
                    Twitter
                    </v-tooltip>
                </v-col>
            </v-row>
        </v-container>
    </div>
</template>