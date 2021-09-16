<template>
    <div class="pa-5 grey lighten-4">
        <v-container>
            <v-row>
                <v-col cols="12" sm="8" class="">
                <h3 class="headline font-weight-light primary--text">AGENTS <span class="display-1 font-weight-bold primary--text">&nbsp;CENTRAL</span></h3>
                </v-col>
                <v-col cols="12" sm="4" class="text-right">
                    <v-btn class="primary" @click="addNewAgentsDialog = true" dark><v-icon>mdi-plus</v-icon>&nbsp;Add AGENT</v-btn>
                </v-col>
            </v-row>
            <v-row>
                <v-col cols="12" sm="12" md="4" xl="3" v-for="(data,index) in agents" :key="index">
                    <v-card class="pb-5 rounded-xl" flat>
                        <v-img :src="data.agent_pic" contain height="250"></v-img>
                        <p class="pt-3 text-center px-3 mb-0 font-weight-bold">{{data.agent_name}}</p>
                        <p class="caption mb-1 text-center px-3 font-weight-bold caption">{{data.agent_info.designation}}</p>
                        <div v-for="(item,ind) in data.agent_info.phone_number" :key="ind" class="text-center">
                            <p class="mb-0 caption blue-grey--text" v-if="item !=''"><v-icon color="indigo" size="20" class="">mdi-phone</v-icon>{{item}}</p>
                        </div>
                    </v-card>
                </v-col>
            </v-row>
        </v-container>

        <!-- Add New Community -->
        <v-dialog v-model="addNewAgentsDialog" max-width="900px">
            <v-card class="" style="overflow-x : hidden" min-height="400">
                <v-toolbar dark color="primary" >
                    <v-toolbar-title>Add New Agents</v-toolbar-title>
                    <v-spacer></v-spacer>
                    <v-btn icon dark @click="addNewAgentsDialog = false">
                        <v-icon>mdi-close</v-icon>
                    </v-btn>
                </v-toolbar>
                <v-container>
                    <v-form ref="form">
                        <v-row>
                            <v-col cols="12" sm="12" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Agent Name</p>
                                <v-text-field dense outlined v-model="agent.agent_name" placeholder="Agent Name" :rules="genericRule"></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="12" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Designation</p>
                                <v-text-field dense outlined v-model="agent.agent_info.designation" placeholder="Designation" :rules="genericRule"></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="12" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Banner Image</p>
                                <span v-if="agent.agent_pic != ''">
                                    <v-btn small class="indigo mr-2" dark @click="openImage(agent.agent_pic)">Open Banner</v-btn>&nbsp;
                                </span>
                                <v-file-input outlined dense placeholder="Attach Banner Image" @change="onUploadAgentImage" v-else>
                                    <template v-slot:selection="{ text }">
                                        <v-chip small label color="primary" >
                                            {{ text }}
                                        </v-chip>
                                    </template>
                                </v-file-input>
                            </v-col>
                            <v-col cols="12" sm="12" md="4" class="py-0">
                                <v-text-field outlined dense v-model="phn1" placeholder="Add Phone Number" :rules="genericRule"></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="12" md="4" class="py-0">
                                <v-text-field outlined dense v-model="phn2" placeholder="Add Phone Number"></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="12" md="4" class="py-0">
                                <v-text-field outlined dense v-model="phn3" placeholder="Add Phone Number"></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="12" class="pt-6 text-center">
                                <v-btn dark class="primary" block @click="addAgent" > Save </v-btn>
                            </v-col>
                        </v-row>
                    </v-form>
                </v-container>
            </v-card>
        </v-dialog>
        <!-- Dialog overlay -->
        <v-row justify="center">
            <v-dialog v-model="dialog_overlay" persistent max-width="400">
                <v-card color="primary" dark class="pa-10">
                    <v-card-text>
                        <p>Adding New Agent. Hang in Tight</p> 
                        <v-progress-linear indeterminate color="white" class="mb-0"></v-progress-linear>
                    </v-card-text>
                </v-card>
            </v-dialog>
        </v-row>
        
    </div>
</template>

<script>
export default {
    data(){
        return{
            addNewAgentsDialog:false,
            agents:[],
            agent:{
                agent_pic:'',
                agent_name:'',
                agent_info:{
                    phone_number :[]
                }
            },
            phn1:'',
            phn2:'',
            phn3:'',
            dialog_overlay:false,
            uploadAgentImage:'',
            genericRule: [
                v => !!v || 'This field is Required'
            ],
            fileRules: [
                v => !!v || 'This field is required',
                v => (v && v.length > 0) || 'This field is required',
            ],
        }
    },
    mounted(){
        this.getData()
    },
    methods:{
        async getData(){
            await this.$axios.$get("teams/all")
            .then(res =>{
                this.agents = res
                console.log(res)
            }).catch()
        },
        async addAgent(){
            if(this.$refs.form.validate()){
                this.dialog_overlay = true

                this.agent.agent_info.phone_number.push(this.phn1,this.phn2,this.phn3)
                await this.attachBannerImage()
                console.log(this.agent)

                this.$axios.$post('teams/add-item/', this.agent)
                .then(async res=>{
                    await this.getData()
                    this.dialog_overlay = false
                    this.addNewAgentsDialog = false
                    this.$router.go()
                }).catch(e => console.log(e))
            }
        },
        onUploadAgentImage(event) {
            this.uploadAgentImage = event
        },
        async attachBannerImage(){
            if(this.uploadAgentImage.name){
                let upload_meta = {
                    file: this.uploadAgentImage,
                    filename: this.uploadAgentImage.name
                }
                await this.uploadFile(upload_meta)
                let attach = {
                    link:this.link_url,
                    filename:this.link_filename,
                    time: new Date()
                }
                this.agent.agent_pic = this.link_url
            }
        },
        async uploadFile(val) {
            console.log(val)
            const fd = new FormData();
            fd.append('a',val.file)
            fd.append('b',val.file.name)
            fd.append('folder',"agents/"+this.agent.agent_name)

            await this.$axios.$post("/teams/upload-files", fd)
            .then(res => {
                this.link_url = res.url
                this.link_filename = res.name
            })
            .catch(e => console.log(e));
        },
    },
    computed:{
        
    }
}
</script>