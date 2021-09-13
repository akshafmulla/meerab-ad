<template>
    <div class="pa-5 grey lighten-4">
        <v-container>
            <v-row>
                <v-col cols="12" sm="8" class="">
                    <h3 class="headline font-weight-light primary--text">COMMUNITY <span class="display-1 font-weight-bold primary--text">&nbsp;CENTRAL</span></h3>
                </v-col>
                <v-col cols="12" sm="4" class="text-right">
                    <v-btn class="primary" @click="addNewCommunityDialog = true" dark><v-icon>mdi-plus</v-icon>&nbsp;Add Community</v-btn>
                </v-col>
            </v-row>
            <v-row>
                <v-col cols="12" sm="12" md="3" xl="2" v-for="(data,index) in communities" :key="index">
                    <v-card class="pb-5" flat>
                        <v-img :src="data.community_banner" height="300"></v-img>
                        <p class="pt-3 text-center px-3 font-weight-bold">{{data.community_name}}</p>
                    </v-card>
                </v-col>
            </v-row>
        </v-container>


        <!-- Add New Community -->
        <v-dialog v-model="addNewCommunityDialog" max-width="900px">
            <v-card class="" style="overflow-x : hidden" min-height="400">
                <v-toolbar dark color="primary" >
                    <v-toolbar-title>Add New Community</v-toolbar-title>
                    <v-spacer></v-spacer>
                    <v-btn icon dark @click="addNewCommunityDialog = false">
                        <v-icon>mdi-close</v-icon>
                    </v-btn>
                </v-toolbar>
                <v-container>
                    <v-form ref="form">
                        <v-row>
                            <v-col cols="12" sm="12" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Community Name <span class="red--text">(Add unique name)</span></p>
                                <v-text-field dense outlined v-model="community.community_name" placeholder="Community Name" :rules="genericRule"></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="12" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Banner Image</p>
                                <span v-if="community.community_banner != ''">
                                    <v-btn small class="indigo mr-2" dark @click="openImage(community.community_banner)">Open Banner</v-btn>&nbsp;
                                </span>
                                <v-file-input outlined dense placeholder="Attach Banner Image" @change="onUploadBannerImage" v-else>
                                    <template v-slot:selection="{ text }">
                                        <v-chip small label color="primary" >
                                            {{ text }}
                                        </v-chip>
                                    </template>
                                </v-file-input>
                            </v-col>
                            <v-col cols="12" sm="12" class="pt-6 text-center">
                                <v-btn dark class="primary" block @click="addCommunity" > Save </v-btn>
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
                        <p>Adding the Property. Hang in Tight</p> 
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
            addNewCommunityDialog:false,
            communities:[],
            community:{
                community_banner:'',
                community_name:''
            },
            dialog_overlay:false,
            uploadBannerImage:'',
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
            await this.$axios.$get("communities/all")
            .then(res =>{
                this.communities = res
                console.log(res)
            }).catch()
        },
        async addCommunity(){
            if(this.$refs.form.validate()){
                this.dialog_overlay = true

                await this.attachBannerImage()
                console.log(this.community)

                this.$axios.$post('communities/add-item/', this.community)
                .then(async res=>{
                    await this.getData()
                    this.dialog_overlay = false
                    this.addNewCommunityDialog = false
                }).catch(e => console.log(e))
            }
        },
        onUploadBannerImage(event) {
            this.uploadBannerImage = event
        },
        async attachBannerImage(){
            if(this.uploadBannerImage.name){
                let upload_meta = {
                    file: this.uploadBannerImage,
                    filename: this.uploadBannerImage.name
                }
                await this.uploadFile(upload_meta)
                let attach = {
                    link:this.link_url,
                    filename:this.link_filename,
                    time: new Date()
                }
                this.community.community_banner = this.link_url
            }
        },
        async uploadFile(val) {
            console.log(val)
            const fd = new FormData();
            fd.append('a',val.file)
            fd.append('b',val.file.name)
            fd.append('folder',"communities/"+this.community.community_name)

            await this.$axios.$post("/communities/upload-files", fd)
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