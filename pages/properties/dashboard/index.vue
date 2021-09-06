<template>
    <div class="pa-5 grey lighten-4">
        <!-- {{properties}} -->
        <v-container>
            <v-row>
                <v-col cols="12" sm="8" class="">
                <h3 class="headline font-weight-light primary--text">PROPERTIES <span class="display-1 font-weight-bold primary--text">&nbsp;CENTRAL</span></h3>
                </v-col>
                <v-col cols="12" sm="4" class="text-right">
                    <v-btn class="primary" @click="addNewPropertyDialog = true" dark>
                        <v-icon>mdi-plus</v-icon>&nbsp;Add Project</v-btn>
                </v-col>
            </v-row>
            <v-row>
                <v-col cols="12" sm="12" md="6">
                    <v-card class="rounded-xl" flat min-height="800">
                        <v-card-title class="pb-2">
                            <span class="font-weight-bold mt-n4 primary--text">Property List</span>
                            <v-spacer></v-spacer>
                            <v-text-field outlined dense append-icon="mdi-magnify" v-model="searchProperty" placeholder="Search here..."></v-text-field>
                        </v-card-title>
                        <v-divider class="mt-n3 mx-5"></v-divider>
                    </v-card>
                </v-col>
                <v-col cols="12" sm="12" md="6">
                    <v-card class="rounded-xl pt-3" flat min-height="800">
                        <v-card-title class="">
                            <span class="font-weight-bold mt-n4 primary--text">Property Information</span>
                            <v-spacer></v-spacer>
                            <v-btn fab x-small @click="toggleEdit = !toggleEdit" :color="!toggleEdit ? 'primary' : 'red'"><v-icon color="white">{{!toggleEdit ? 'mdi-pencil' : 'mdi-close'}}</v-icon></v-btn>
                        </v-card-title>
                        <v-divider class="mx-5"></v-divider>
                    </v-card>
                </v-col>
            </v-row>
       </v-container>

        <!-- Add New Property -->
        <v-dialog v-model="addNewPropertyDialog" fullscreen hide-overlay transition="dialog-bottom-transition" >
            <v-card>
                <v-toolbar dark color="primary" >
                    <!-- <v-toolbar-title>ADD NEW PROPERTY</v-toolbar-title> -->
                    <v-spacer></v-spacer>
                    <v-btn icon dark @click="addNewPropertyDialog = false">
                        <v-icon>mdi-close</v-icon>
                    </v-btn>
                </v-toolbar>
                <v-container>
                    <p class="display-1 primary--text pt-5">Add New Property</p>
                    <v-form ref="form">
                        <v-row>
                            <v-col cols="12" sm="12" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Property Name <span class="red--text">(Add unique name)</span></p>
                                <v-text-field dense outlined v-model="projects.property_name" placeholder="Property Name" :rules="genericRule"></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="6" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Community</p>
                                <v-text-field dense outlined v-model="projects.community" placeholder="Community" :rules="genericRule"></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="6" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Developer</p>
                                <v-select :items="developerList" dense outlined v-model="projects.developer" placeholder="Developer" :rules="genericRule"></v-select>
                            </v-col>
                            <v-col cols="12" sm="6" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Starting Price</p>
                                <v-text-field dense outlined v-model="projects.starting_price" type="number" placeholder="Starting Price" :rules="genericRule"></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="6" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Bedroom Options</p>
                                <v-select :items="roomsList" multiple dense outlined v-model="projects.rooms" placeholder="Bedroom" :rules="fileRules"></v-select>
                            </v-col>
                            <v-col cols="12" sm="6" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Property Type</p>
                                <v-select :items="propertyTypeList" dense outlined v-model="projects.property_type" placeholder="Property Type" :rules="genericRule"></v-select>
                            </v-col>
                            <v-col cols="12" sm="6" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Area Range</p>
                                <v-range-slider v-model="range" :max="max" :min="min" hide-details class="align-center">
                                    <template v-slot:prepend>
                                        <v-text-field :value="range[0]" class="mt-0 pt-0" hide-details single-line type="number" outlined dense @change="$set(range, 0, $event)"></v-text-field>
                                    </template>
                                    <template v-slot:append>
                                        <v-text-field :value="range[1]" class="mt-0 pt-0" hide-details single-line type="number" outlined dense @change="$set(range, 1, $event)"></v-text-field>
                                    </template>
                                </v-range-slider>
                            </v-col>
                            <v-col cols="12" sm="6" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Ammenities</p>
                                <v-autocomplete :items="ammenitiesList" multiple dense outlined v-model="projects.ammenities" placeholder="Ammenities" :rules="fileRules"></v-autocomplete>
                            </v-col>
                            <v-col cols="12" sm="6" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">3D Property Link</p>
                                <v-text-field dense outlined v-model="projects.property_3d_link" placeholder="3D Property Link"></v-text-field>
                            </v-col>
                            <v-col cols="12" sm="6" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Banner Image <span class="red--text">(Size : 1920px * 768px)</span></p>
                                <span v-if="projects.banner_img != ''">
                                    <v-btn small class="pink" dark @click="openImage(projects.banner_img)">Open Image</v-btn>&nbsp;
                                </span>
                                <v-file-input outlined dense placeholder="Attach Banner Image" @change="onUploadBannerImage" v-else>
                                    <template v-slot:selection="{ text }">
                                        <v-chip small label color="primary" >
                                            {{ text }}
                                        </v-chip>
                                    </template>
                                </v-file-input>
                            </v-col>
                            <v-col cols="12" sm="6" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Property Images</p>
                                <span v-if="projects.property_pics.length > 0">
                                    <span v-for="(data,index) in projects.property_pics" :key="index">
                                        <v-btn small class="pink" dark @click="openImage(data.link)">Open Image</v-btn>&nbsp;
                                    </span>
                                </span>
                                <v-file-input outlined multiple dense placeholder="Attach Multiple Property Image" @change="onUploadPropertyPics" :rules="fileRules" v-else>
                                    <template v-slot:selection="{ text }">
                                        <v-chip small label color="primary" >
                                            {{ text }}
                                        </v-chip>
                                    </template>
                                </v-file-input>
                            </v-col> 
                            <v-col cols="12" sm="12" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Overview</p>
                                <div v-for="(data,index) in projects.overview" :key="index">
                                    <v-row>
                                        <v-col cols="12" sm="12" md="10" class="py-0">
                                            <v-text-field dense outlined v-model="data.text" placeholder="Text Line" :rules="genericRule" v-if="data.type == 'text'"></v-text-field>
                                            <div v-for="(item,ind) in data.text" :key="ind" v-else>
                                                <v-row>
                                                    <v-col cols="12" sm="12" md="6" class="py-0">
                                                        <v-text-field dense outlined v-model="item.val" placeholder="Add Pointers" :rules="genericRule"></v-text-field>
                                                    </v-col>
                                                    <v-col cols="12" sm="12" md="3" class="py-0">
                                                        <v-btn class="primary mr-2" x-small fab outlined dark @click="pushNewPointer(index,'overview')"><v-icon>mdi-plus</v-icon></v-btn>
                                                        <v-btn class="red white--text" x-small fab dark @click="removePointer(index,ind,'overview')"><v-icon>mdi-close</v-icon></v-btn>
                                                    </v-col>
                                                </v-row>
                                            </div>
                                        </v-col>
                                        <v-col cols="12" sm="12" md="2" class="pb-0 pt-2">
                                            <v-btn class="primary mr-2" x-small outlined dark @click="pushNew('text','overview')">Add New Line</v-btn>
                                            <v-btn class="indigo darken-1 mr-2" x-small outlined dark @click="pushNew('list','overview')">Add List</v-btn>
                                            <v-btn class="red white--text" x-small dark @click="removeNewObject(index,'overview')">Remove</v-btn>
                                        </v-col>
                                    </v-row>
                                </div>
                            </v-col>
                            <v-col cols="12" sm="12" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Location</p>
                                <div v-for="(data,index) in projects.location" :key="index">
                                    <v-row>
                                        <v-col cols="12" sm="12" md="10" class="py-0">
                                            <v-text-field dense outlined v-model="data.text" placeholder="Text Line" :rules="genericRule" v-if="data.type == 'text'"></v-text-field>
                                            <div v-for="(item,ind) in data.text" :key="ind" v-else>
                                                <v-row>
                                                    <v-col cols="12" sm="12" md="6" class="py-0">
                                                        <v-text-field dense outlined v-model="item.val" placeholder="Add Pointers" :rules="genericRule"></v-text-field>
                                                    </v-col>
                                                    <v-col cols="12" sm="12" md="3" class="py-0">
                                                        <v-btn class="primary mr-2" x-small fab outlined dark @click="pushNewPointer(index,'location')"><v-icon>mdi-plus</v-icon></v-btn>
                                                        <v-btn class="red white--text" x-small fab dark @click="removePointer(index,ind,'location')"><v-icon>mdi-close</v-icon></v-btn>
                                                    </v-col>
                                                </v-row>
                                            </div>
                                        </v-col>
                                        <v-col cols="12" sm="12" md="2" class="pb-0 pt-2">
                                            <v-btn class="primary mr-2" x-small outlined dark @click="pushNew('text','location')">Add New Line</v-btn>
                                            <v-btn class="indigo darken-1 mr-2" x-small outlined dark @click="pushNew('list','location')">Add List</v-btn>
                                            <v-btn class="red white--text" x-small dark @click="removeNewObject(index,'location')">Remove</v-btn>
                                        </v-col>
                                    </v-row>
                                </div>
                            </v-col>
                            <v-col cols="12" sm="12" class="pt-6 text-center">
                                <v-btn dark class="primary" block @click="addProperty" > Save </v-btn>
                            </v-col>
                        </v-row>
                    </v-form>
                </v-container>
            </v-card>
        </v-dialog>
    </div>
</template>

<script>
export default {
    data(){
        return{
            toggleEdit:false,
            searchProperty:'',
            min: 500,
            max: 50000,
            range:[1000,5000],
            genericRule: [
                v => !!v || 'This field is Required'
            ],
            fileRules: [
                v => !!v || 'This field is required',
                v => (v && v.length > 0) || 'This field is required',
            ],
            addNewPropertyDialog: false,
            projects:{
                property_name:'',
                community:'',
                developer:'',
                starting_price:0,
                rooms:[],
                property_type:'',
                area:[],
                overview:[
                    {text:'',type:'text'}
                ],
                location:[
                    {text:'',type:'text'}
                ],
                ammenities:[],
                banner_img:'',
                property_pics:[],
                property_details:{},
                property_3d_link:'',
            },
            developerList:['Emaar','Sobha','Damac','Meeras','Nakheel'],
            propertyTypeList:["Villas","Apartments","Townhouse"],
            roomsList:[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15],
            ammenitiesList:["Kindergarten","2 Cafes","3 restaurants","Clinic","Golf Club","Tennis Courts","State-of-the-art Gym","Bali-inspired Pool","Pool Pavilion","Hammocks","Sun Lounge Terraces","Clubhouse","Barbeque Area","Outdoor Wellness Area","Reception service ","Concierge service ","Smart home technology ","Video security ","Common courtyard ","Common garden ","Meeting room ","Gymnasium ","Steam room ","Sauna ","Jacuzzi ","Infinity Pool ","Overflow pool ","Standard pool ","Pet Friendly ","Games room ","Kids club ","Restaurant Retail area","Reception service ","Smart home technology ","Video security ","Common courtyard ","Common garden ","Meeting room ","Gymnasium ","Steam room ","Sauna ","Jacuzzi ","Standard pool ","Pet Friendly ","Games room ","Kids club ","Restaurant Retail area","ROOFTOP SWIMMING POOL","GYMNASIUM","HEALTH CLUB","KIDS’ CLUB & PLAY AREA","18-HOLE CHAMPIONSHIP GOLF COURSE","DUBAI POLO & EQUESTRIAN CLUB","GATED COMMUNITY","LEISURE CENTRE","KIDS' PLAY AREA","Free Chiller","Central A/C","Gym","Children pool","Basement","CCTV cameras","Covered Parking","Children play area","Landmark view","Lobby in building","Mosque / prayer room","Security","Shared pool","Supermarket nearby","Community center","Gym","Covered Parking","Cycling tracks","Children play area","Jogging tracks","Pets allowed","Shared pool","Supermarket nearby","INFINITY SWIMMING POOL","STATE-OF-THE-ART GYM","CIGAR LOUNGE","LIBRARY","MOVIE THEATRE","GOLF SIMULATOR","GAME ROOM","Gymnasium","Children's play area","Children's Play Area","Restaurants","Restaurants","Shopping mall","Shopping Mall","Beach Access","Beach Access","Jogging Tracks","Jogging Tracks","18-HOLE GOLF COURSE","1,450,000 SQM PARKS & OPEN SPACES","DUBAI HILLS PARK","DUBAI HILLS MALL","CONCIERGE SERVICE","Gym","Shared spa","Fine Dining","Private Pool","Fitness Centre","Dubai fountain","Retail Outlets","Covered Parking","Landscaped Garden","Private Beach Access","Waterfront Living","Resort-Style Amenities","Private Beach Access"],
            link_filename:'',
            link_url:''
        }
    },
    // async asyncData({app, store}) {
    //     let propertiesData = await app.$axios.$get("/properties/all")
    //     return {
    //         properties: propertiesData
    //     }
    // },
    mounted(){

    },
    methods:{
        pushNew(val,objName){
            let obj = {
                type: val
            }
            val == 'text' ? obj.text = '' : obj.text = [{val:''}]
            objName == 'overview' ? this.projects.overview.push(obj) : this.projects.location.push(obj)
        },
        removeNewObject(index,objName){
            objName == 'overview' ? this.projects.overview.splice(index,1) : this.projects.location.splice(index,1)
        },
        pushNewPointer(index,objName){
            let obj = {
                val : ''
            }
            objName == 'overview' ? this.projects.overview[index].text.push(obj) : this.projects.location[index].text.push(obj)
        },
        removePointer(index,ind,objName){
            objName == 'overview' ? this.projects.overview[index].text.splice(ind,1) : this.projects.location[index].text.splice(ind,1)
        },
        async addProperty(){
            if(this.$refs.form.validate()){

                this.projects.area = this.range
                console.log(this.projects)

                // await attachBannerImage()
                // await attachPropertyImages()
                // this.$axios.$post('properties/add-item/', this.projects).then(res=>console.log(res)).catch(e => console.log(e))

                this.addNewPropertyDialog = false
            }
        },
        onUploadBannerImage(event) {
            this.uploadBannerImage = event
        },
        onUploadPropertyPics(event) {
            this.uploadPropertyImages = event
        },
        async attachBannerImage(){
            let upload_meta = {
                file: this.uploadPropertyImages,
                filename: this.uploadPropertyImages.name
            }
            await this.uploadFile(upload_meta)
            let attach = {
                link:this.link_url,
                filename:this.link_filename,
                time: new Date()
            }
            this.projects.banner_img = this.link_url
            this.projects.property_pics.push(attach)
        },
        async attachPropertyImages(){
            for(let i=0;i< this.uploadPropertyImages.length; i++){
                if(this.uploadPropertyImages[i].name != undefined){
                    let upload_meta = {
                        file: this.uploadPropertyImages[i],
                        filename: this.uploadPropertyImages[i].name
                    }
                    await this.uploadFile(upload_meta)
                    let attach = {
                        link:this.link_url,
                        filename:this.link_filename,
                        time: new Date()
                    }
                    this.projects.property_pics.push(attach)
                }
            }
        },
        async uploadFile(val) {
            const fd = new FormData();
            fd.append('a',val.file,val.name)
            fd.append('b',this.user._id+Date.now()+val.file.name)
            fd.append('folder',"properties/"+this.projects.property_name)

            await this.$axios.$post("/properties/upload-file", fd)
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