<template>
    <div class="pa-5 grey lighten-4">
        <v-container>
            <v-row>
                <v-col cols="12" sm="8" class="">
                <h3 class="headline font-weight-light primary--text">PROPERTIES <span class="display-1 font-weight-bold primary--text">&nbsp;CENTRAL</span></h3>
                </v-col>
                <v-col cols="12" sm="4" class="text-right">
                    <v-btn class="purple" @click="showBanner = true" dark>Show Home Banner</v-btn>
                    <v-btn class="primary" @click="addNewPropertyDialog = true" dark><v-icon>mdi-plus</v-icon>&nbsp;Add Project</v-btn>
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
                        <v-list two-line class="scroll px-3" style="max-height : 800px;"  v-if="visibleProperties.length > 0">
                            <template v-for="(data, index) in visibleProperties">
                                <v-divider :key="data._id" class="grey lighten-3" :inset ="true" v-if="index != 0"></v-divider>
                                <v-list-item :key="index" @click="selectProperty(data)">
                                    <v-avatar size="50">
                                        <img :src="getImage(data.banner_img)" >
                                    </v-avatar>
                                    <v-list-item-content class="pl-4">
                                        <v-list-item-title>{{data.property_name}}</v-list-item-title>
                                        <v-list-item-subtitle class="pt-1">{{data.community}}</v-list-item-subtitle>
                                    </v-list-item-content>
                                    <v-list-item-action class="pl-2 text-right">
                                        <v-list-item-title><span class="grey--text caption"><v-icon class="mt-n1" color="primary" size="15">mdi-warehouse</v-icon>&nbsp;{{data.property_type}}</span> </v-list-item-title>
                                        <v-chip class="black white--text" small>{{data.developer}}</v-chip>
                                    </v-list-item-action>
                                </v-list-item>
                            </template>
                        </v-list>
                        <v-list v-else>
                            <p class="pa-4 caption">Currently, there are no Properties Listed here!</p>
                        </v-list>
                        <v-row justify="center">
                            <v-col md="6">
                                <div class="pb-3" style="position: absolute; bottom:0;">
                                    <v-pagination class="pt-2" v-model="page" :length="Math.ceil(filterText.length/perPage)" :total-visible="5" circle v-if="filterText != undefined"></v-pagination>
                                </div>
                            </v-col>
                        </v-row>
                    </v-card>
                </v-col>
                <v-col cols="12" sm="12" md="6">
                    <v-card class="rounded-xl pt-3" flat min-height="800">
                        <v-card-title class="">
                            <span class="font-weight-bold mt-n4 primary--text">Property Information</span>
                            <v-spacer></v-spacer>
                            <!-- <v-btn fab x-small @click="toggleEdit = !toggleEdit" :color="!toggleEdit ? 'primary' : 'red'"><v-icon color="white">{{!toggleEdit ? 'mdi-pencil' : 'mdi-close'}}</v-icon></v-btn> -->
                            <v-btn x-small class="indigo white--text" @click="updatePropertyToBanner(true)" v-if="selectedProject && selectedProject.home_banner_highlight == false">Add to Banner</v-btn>
                            <v-btn x-small class="red white--text" @click="updatePropertyToBanner(false)"  v-else-if="selectedProject && selectedProject.home_banner_highlight == true">Remove from Banner</v-btn>
                        </v-card-title>
                        <v-divider class="mx-5"></v-divider>
                        <div class="px-3 scroll" v-if="selectedProject" style="max-height:700px;">
                            <v-img :src="selectedProject.banner_img" max-height="200"></v-img>
                            <h3 class="primary--text text-center pt-2">{{selectedProject.property_name}} &emsp;</h3>
                            <p class="mb-0 text-center"><v-chip class="indigo white--text" x-small>{{selectedProject.property_type}}</v-chip></p>
                            <p class="mb-1 caption text-center">{{selectedProject.community}} by {{selectedProject.developer}}</p>
                            <p class="caption text-center"><v-icon class="mt-n1" color="primary" size="15">mdi-warehouse</v-icon>&nbsp;<span v-for="(item, i) in selectedProject.rooms" :key="i">{{item}}<span v-if="i < selectedProject.rooms.length - 1">,&nbsp;</span> </span> Rooms&emsp;&emsp;<v-icon color="green" size="15" class="mt-n1">mdi-cash</v-icon>&nbsp;Starting {{selectedProject.starting_price | amountFormatter}} AED</p>
                            <h4 class="pl-3 blue-grey--text">Overview</h4>
                            <v-row class="pl-3 caption" v-for="(data,index) in selectedProject.overview" :key="index">
                                <v-col cols="12" sm="12" md="12" class="pb-0">    
                                    <p class="mb-0" v-if="data.type == 'text'">{{data.text}}</p>
                                    <v-container v-else>
                                        <v-row>
                                            <v-col class="py-0" cols="12" sm="12" md="6" v-for="(item,ind) in data.text" :key="ind">
                                                <ul>
                                                    <li>{{item.val}}</li>
                                                </ul>
                                            </v-col>
                                        </v-row>
                                    </v-container>
                                </v-col>
                            </v-row>
                            <h4 class="py-4 pl-3 blue-grey--text">Property Pictures</h4>
                            <v-row class="pl-3">
                                <v-col cols="12" sm="12" md="3"  v-for="(data,index) in selectedProject.property_pics" :key="index">
                                    <v-img :src="data.link" max-height="150" max-width="150"/>
                                </v-col>
                            </v-row>
                            <h4 class="pt-3 pl-3 blue-grey--text">Location</h4>
                            <v-row class="pl-3 caption" v-for="(data,index) in selectedProject.location" :key="index">
                                <v-col cols="12" sm="12" md="12" class="pb-0">    
                                    <p class="mb-0" v-if="data.type == 'text'">{{data.text}}</p>
                                    <v-container v-else>
                                        <v-row>
                                            <v-col class="py-0" cols="12" sm="12" md="6" v-for="(item,ind) in data.text" :key="ind">
                                                <ul>
                                                    <li>{{item.val}}</li>
                                                </ul>
                                            </v-col>
                                        </v-row>
                                    </v-container>
                                </v-col>
                            </v-row>
                            <h4 class="pt-3 pl-3 blue-grey--text">Ammenities</h4>
                            <v-container>
                                <v-row class="pl-3 caption">
                                    <v-col cols="12" sm="12" md="6" class="pt-0 pb-1"  v-for="(data,index) in selectedProject.ammenities" :key="index">    
                                        <ul>
                                            <li>{{data}}</li>
                                        </ul>
                                    </v-col>
                                </v-row>
                            </v-container>
                        </div>
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
                                <p class="caption font-weight-bold primary--text mb-0">Neighbourhood</p>
                                <v-autocomplete :items="neighbourhoodList"  dense outlined v-model="projects.neighbourhood" placeholder="Neighbourhood" :rules="genericRule"></v-autocomplete>
                            </v-col>
                            <v-col cols="12" sm="6" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Community</p>
                                <v-autocomplete :items="communities" item-text="community_name" item-value="community_name"  dense outlined v-model="projects.community" placeholder="Community"></v-autocomplete>
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
                                    <v-btn small class="indigo mr-2" dark @click="openImage(projects.banner_img)">Open Banner</v-btn>&nbsp;
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
                                        <v-btn small class="pink mr-2" dark @click="openImage(data.link)">Open Images</v-btn>&nbsp;
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
                            <v-col cols="12" sm="6" class="py-0">
                                <p class="caption font-weight-bold primary--text mb-0">Floor Plan</p>
                                <span v-if="projects.floor_plan.length > 0">
                                    <span v-for="(data,index) in projects.floor_plan" :key="index">
                                        <v-btn small class="blue mr-2" dark @click="openImage(data.link)">Open Images</v-btn>&nbsp;
                                    </span>
                                </span>
                                <v-file-input outlined multiple dense placeholder="Attach Multiple Floor Plan Image" @change="onUploadFloorPanPics" v-else>
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

        <!-- Show Banner -->
        <v-dialog v-model="showBanner" max-width="900px">
            <v-card class="" style="overflow-x : hidden" min-height="400">
                <v-toolbar dark color="primary" >
                    <v-toolbar-title>Home Banner Properties</v-toolbar-title>
                    <v-spacer></v-spacer>
                    <v-btn icon dark @click="showBanner = false">
                        <v-icon>mdi-close</v-icon>
                    </v-btn>
                </v-toolbar>
                <v-container>
                    <v-list two-line class="scroll px-3" style="max-height : 800px;"  v-if="fetchBannerProperties.length > 0">
                        <template v-for="(data, index) in fetchBannerProperties">
                            <v-divider :key="data._id" class="grey lighten-3" :inset ="true" v-if="index != 0"></v-divider>
                            <v-list-item :key="index" @click="selectProperty(data)">
                                <v-avatar size="50">
                                    <img :src="getImage(data.banner_img)" >
                                </v-avatar>
                                <v-list-item-content class="pl-4">
                                    <v-list-item-title>{{data.property_name}}</v-list-item-title>
                                    <v-list-item-subtitle class="pt-1">{{data.community}}</v-list-item-subtitle>
                                </v-list-item-content>
                                <v-list-item-action class="pl-2 text-right">
                                    <v-list-item-title><span class="grey--text caption"><v-icon class="mt-n1" color="primary" size="15">mdi-warehouse</v-icon>&nbsp;{{data.property_type}}</span> </v-list-item-title>
                                    <v-chip class="black white--text" small>{{data.developer}}</v-chip>
                                </v-list-item-action>
                            </v-list-item>
                        </template>
                    </v-list>
                    <v-list v-else>
                        <p class="pa-4 caption">Currently, there are no Properties Listed here!</p>
                    </v-list>
                    <!-- {{fetchBannerProperties}} -->
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
            showBanner:false,
            dialog_overlay:false,
            toggleEdit:false,
            searchProperty:'',
            min: 500,
            max: 50000,
            range:[1000,5000],
            page:1,
            perPage:8,
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
                floor_plan:[],
                property_details:{},
                property_3d_link:'',
                home_banner_highlight : false
            },
            selectedProject:{
                rooms:[],
                area:[],
                overview:[],
                location:[],
                ammenities:[],
                property_pics:[],
                property_details:{}
            },
            properties:[],
            developerList:['Emaar','Sobha','Damac','Meeras','Nakheel'],
            propertyTypeList:["Villas","Apartments","Townhouse"],
            roomsList:[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15],
            neighbourhoodList:["Area","Akoya Oxygen","Al Barari","Al Barsha","Al Barsha 2","Al Barsha 3","Al Barsha South","Al Barsha South 4","Al Furjan","Al Garhoud","Al Karama","Al Khail Heights","Al Khawaneej","Al Nahda","Al Quoz","Al quoz 4","Al Qusais","Al satwa","Al sufouh","Al wasl","Arabian Ranches","Arabian Ranches 1","Arabian Ranches 2","Arabian Ranches 3","Arjan","Barsha heights (Tecom)","Bluewaters Island","Bur Dubai","Business Bay","City Walk","Creek Beach","Damac Hills","Deira","Discovery Gardens","Duabi Creek Harbour (DCH)","Duabi Downtown","Duabi Hills Estate (DHE)","Duabi Land","Duabi Marina","Duabi South","Dubai Festival City (DFC)","Dubai International Financial Centre(DIFC)","Dubai Investment Park (DIP)","Dubai Media City","Dubai Science Park","Dubai Silicon Oasis (DSO)","Dubai Sports City","Elan, Tilal Al Ghaf","Emaar Beachfront","Emaar South","Emirates Hills","Emirates Living","IMPZ","International City","Jebel Ali","Jumeirah","Jumeirah Bay Island","Jumeirah Beach Residence (JBR)","Jumeirah Golf Estates (JGE)","Jumeirah Island","Jumeirah Lake Towers (JLT)","Jumeirah Park","Jumeirah Village Circle (JVC)","Jumeirah Village Triangle(JVT)","La Mer","Liwan","Madinat Jumeirah Living (MJL), Umm Suqueim","Majan","Meadows","Meydan","Mina Rashid","Mira","Mira 1","Mira 4","Mira oasis","Mira oasis 1","Mira oasis 2","Mira oasis 3","Mirdif","Mohammad Bin Rashid Al Maktoum (MBR)","Mohammad Bin Zayed Road","Motor City","Mudon","Nad Al Sheba","Nshama Town Square","Old Town","Palm Jumeirah","Port Saeed","Queue Point","Saadiyat Island","Sheikh Zayed Road","Sobha Hartland MBR","The Greens","The Hills","The Lagoons","The Lakes","The Springs","The Valley","The Views","The Villa","The World Islands","Umm Ramool","Umm Suqueim","Villanova","World Trade Centre","Zabeel"],
            ammenitiesList:["Kindergarten","2 Cafes","3 restaurants","Clinic","Golf Club","Tennis Courts","State-of-the-art Gym","Bali-inspired Pool","Pool Pavilion","Hammocks","Sun Lounge Terraces","Clubhouse","Barbeque Area","Outdoor Wellness Area","Reception service ","Concierge service ","Smart home technology ","Video security ","Common courtyard ","Common garden ","Meeting room ","Gymnasium ","Steam room ","Sauna ","Jacuzzi ","Infinity Pool ","Overflow pool ","Standard pool ","Pet Friendly ","Games room ","Kids club ","Restaurant Retail area","Reception service ","Smart home technology ","Video security ","Common courtyard ","Common garden ","Meeting room ","Gymnasium ","Steam room ","Sauna ","Jacuzzi ","Standard pool ","Pet Friendly ","Games room ","Kids club ","Restaurant Retail area","ROOFTOP SWIMMING POOL","GYMNASIUM","HEALTH CLUB","KIDS’ CLUB & PLAY AREA","18-HOLE CHAMPIONSHIP GOLF COURSE","DUBAI POLO & EQUESTRIAN CLUB","GATED COMMUNITY","LEISURE CENTRE","KIDS' PLAY AREA","Free Chiller","Central A/C","Gym","Children pool","Basement","CCTV cameras","Covered Parking","Children play area","Landmark view","Lobby in building","Mosque / prayer room","Security","Shared pool","Supermarket nearby","Community center","Gym","Covered Parking","Cycling tracks","Children play area","Jogging tracks","Pets allowed","Shared pool","Supermarket nearby","INFINITY SWIMMING POOL","STATE-OF-THE-ART GYM","CIGAR LOUNGE","LIBRARY","MOVIE THEATRE","GOLF SIMULATOR","GAME ROOM","Gymnasium","Children's play area","Children's Play Area","Restaurants","Restaurants","Shopping mall","Shopping Mall","Beach Access","Beach Access","Jogging Tracks","Jogging Tracks","18-HOLE GOLF COURSE","1,450,000 SQM PARKS & OPEN SPACES","DUBAI HILLS PARK","DUBAI HILLS MALL","CONCIERGE SERVICE","Gym","Shared spa","Fine Dining","Private Pool","Fitness Centre","Dubai fountain","Retail Outlets","Covered Parking","Landscaped Garden","Private Beach Access","Waterfront Living","Resort-Style Amenities","Private Beach Access"],
            link_filename:'',
            link_url:'',
            uploadBannerImage:'',
            uploadPropertyImages:[],
            uploadFloorPlanImages:[],
            communities:[]
        }
    },

    mounted(){
        this.getData()
    },
    methods:{
        
        async getData(){
            await this.$axios.$get("properties/all")
            .then(res =>{
                this.properties = res
                this.selectedProject = res[0]
            }).catch()

            await this.$axios.$get("communities/all")
            .then(res =>{
                this.communities = res
            }).catch()
        },
        openImage(val){
            window.open(val)
        },
        getImage(val){
            let image = '/home-vector.png'
            // if(this.properties.length > 0){
            //     let abc = this.properties.filter(a => a._id == val)
            //     if(abc.length > 0){
            //         if(abc[0].hasOwnProperty('image_url')){
            //             if(abc[0].image_url != '') image = abc[0].image_url
            //         }
            //     }
            // }
            return val != '' ? val : image
        },
        selectProperty(val){
            this.selectedProject = val
        },
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
                this.dialog_overlay = true
                this.projects.area = this.range

                await this.attachBannerImage()
                await this.attachPropertyImages()
                await this.attachFloorPlanImages()
                console.log(this.projects)

                this.$axios.$post('properties/add-item/', this.projects)
                .then(async res=>{
                    await this.getData()
                    this.dialog_overlay = false
                    this.addNewPropertyDialog = false
                    this.$router.go()
                }).catch(e => console.log(e))
            }
        },
        updatePropertyToBanner(flag){
            this.selectedProject.home_banner_highlight = flag
            this.$axios.$put('properties/update/'+this.selectedProject._id, this.selectedProject)
            .then(async res=>{
                console.log(res)
            }).catch(e => console.log(e))
        },
        onUploadBannerImage(event) {
            this.uploadBannerImage = event
        },
        onUploadPropertyPics(event) {
            this.uploadPropertyImages = event
            console.log(this.uploadPropertyImages)
        },
        onUploadFloorPanPics(event) {
            this.uploadFloorPlanImages = event
        },
        async attachBannerImage(){
            console.log(this.uploadBannerImage)
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
                this.projects.banner_img = this.link_url
                this.projects.property_pics.push(attach)
            }
        },
        async attachPropertyImages(){
            for(let i=0;i< this.uploadPropertyImages.length; i++){
                if(this.uploadPropertyImages[i].name){
                    console.log(this.uploadPropertyImages[i])
                    let upload_meta = {
                        file: this.uploadPropertyImages[i],
                        filename: this.uploadPropertyImages[i].name
                    }
                    console.log(upload_meta)
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
        async attachFloorPlanImages(){
            for(let i=0;i< this.uploadFloorPlanImages.length; i++){
                if(this.uploadFloorPlanImages[i].name){
                    console.log(this.uploadFloorPlanImages[i])
                    let upload_meta = {
                        file: this.uploadFloorPlanImages[i],
                        filename: this.uploadFloorPlanImages[i].name
                    }
                    await this.uploadFile(upload_meta)
                    let attach = {
                        link:this.link_url,
                        filename:this.link_filename,
                        time: new Date()
                    }
                    this.projects.floor_plan.push(attach)
                }
            }
        },
        async uploadFile(val) {
            console.log(val)
            const fd = new FormData();
            fd.append('a',val.file)
            fd.append('b',val.file.name)
            fd.append('folder',"properties/"+this.projects.property_name)

            await this.$axios.$post("/properties/upload-files", fd)
            .then(res => {
                this.link_url = res.url
                this.link_filename = res.name
            })
            .catch(e => console.log(e));
        },
    },
    computed:{
        filterText() {
            let properties = this.properties
        
            if (this.searchProperty) {
                var s = this.searchProperty;
                let returnData = _.filter(properties, function (value) {
                    return (
                        value.property_name.toLowerCase().indexOf(s.toLowerCase()) > -1 ||
                        value.community.toLowerCase().indexOf(s.toLowerCase()) > -1 ||
                        value.developer.toLowerCase().indexOf(s.toLowerCase()) > -1 ||
                        value.property_type.toLowerCase().indexOf(s.toLowerCase()) > -1
                    )
                })
                this.selectedProject = returnData[0]
                return returnData
            }
            else{
                this.selectedProject = properties[0]
                return properties
            }
        },
        visibleProperties(){
            return this.filterText.slice((this.page - 1)* this.perPage, this.page* this.perPage)
        },
        fetchBannerProperties(){
            return this.properties.filter(a => a.home_banner_highlight == true)
        }
    }
}
</script>