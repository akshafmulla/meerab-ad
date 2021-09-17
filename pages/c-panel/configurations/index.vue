<template>
    <div class="pa-5 grey lighten-4">
        <v-container>
            <v-row>
                <v-col cols="12" sm="4" class="">
                    <h3 class="headline font-weight-light primary--text">CONFIGURATION <span class="display-1 font-weight-bold primary--text">&nbsp;CENTRAL</span></h3>
                </v-col>
            </v-row>
            <v-row>
                <v-col cols="12" sm="12" md="6">
                    <v-card class="rounded-xl pt-3" flat min-height="800">
                        <v-card-title class="pt-3">
                            <span class="font-weight-bold mt-n4 primary--text">List of Configurations</span>
                        </v-card-title>
                        <v-divider class="mx-5"></v-divider>
                        <p class="mt-3 mb-0 pr-4 text-right" >
                            <v-btn small dark class="primary" @click="saveConfig">Save</v-btn>
                        </p>
                        <v-row class="px-4">
                            <v-col cols="12" sm="12" class="py-0">
                                <p class="blue-grey--text caption font-weight-bold mb-0">Add New Neighbourhood</p>
                                <v-text-field outlined dense v-model="newNeighbour" placeholder="Add New Neighbourhood"></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="12" class="py-0">
                                <p class="blue-grey--text font-weight-bold caption mb-0">Add New Ammenity</p>
                                <v-text-field outlined dense v-model="newAmmenity" placeholder="Add New Ammenity"></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="12" class="py-0">
                                <p class="blue-grey--text font-weight-bold caption mb-0">Add New Developer</p>
                                <v-text-field outlined dense v-model="newDeveloper" placeholder="Add New Developer"></v-text-field>
                            </v-col>
                        </v-row>
                    </v-card>
                </v-col>
                <v-col cols="12" sm="12" md="6">
                    <v-card class="rounded-xl pt-3" flat min-height="800">
                        <v-card-title class="">
                            <span class="font-weight-bold mt-n4 primary--text">Configuration Information</span>
                        </v-card-title>
                        <v-divider class="mx-5"></v-divider>
                        <v-expansion-panels class="pa-3" flat>
                            <v-expansion-panel v-for="(item,i) in accordionList" :key="i" class="scroll" style="max-height : 500px;">
                                <v-expansion-panel-header>
                                    <span class="font-weight-bold blue-grey--text">{{keyNameRegex(i)}}</span>
                                </v-expansion-panel-header>
                                <v-expansion-panel-content>
                                    <v-row>
                                        <v-col cols="12" sm="12" md="6" v-for="(data,index) in item" :key="index" class="py-0">
                                            <li class="caption">{{index + 1}}.&nbsp;{{data}}</li>
                                        </v-col>
                                    </v-row>
                                </v-expansion-panel-content>
                                <v-divider></v-divider>
                            </v-expansion-panel>
                        </v-expansion-panels>
                    </v-card>
                </v-col>
            </v-row>
        </v-container>
        <!-- Snackbar -->
        <v-snackbar v-model="snack" :timeout="3000" :color="snackColor" >
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
            configuration:[],
            newNeighbour:'',
            newAmmenity:'',
            newDeveloper:'',
            snack:false,
            snackText:'',
            snackColor:'',
        }
    },
    mounted(){
        this.getData()
    },
    methods:{
        async getData(){
            await this.$axios.$get("configurations/all")
            .then(res =>{
                this.configuration = res
                console.log(res)
            }).catch()
        },
        reset(){
            this.newNeighbour = ''
            this.newAmmenity = ''
            this.newDeveloper = ''
        },
        keyNameRegex(val){
            return _.startCase(val.replace('List',' List'))
        },
        async saveConfig(){
            if(this.newNeighbour != ''){
                this.configuration[0].neighbourhoodList.push(this.newNeighbour)
            }
            if(this.newAmmenity != ''){
                this.configuration[0].ammenitiesList.push(this.newAmmenity)
            }
            if(this.newDeveloper != ''){
                this.configuration[0].developerList.push(this.newDeveloper)
            }

            await this.$axios.$put("configurations/update/"+ this.configuration[0]._id, this.configuration[0])
            .then(res =>{
                this.configuration[0] = res
                this.snack = true
                this.snackText = 'Update Successful'
                this.snackColor = "success"
                this.reset()
            }).catch()
        }
    },
    computed:{
        accordionList(){
            let config = this.configuration[0]
            return _.omit(config,['_id','createdDate'])
        }
    }
}
</script>