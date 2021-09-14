<template>
    <div class="mx-sm-n5 mx-lg-15">
        <v-sheet class="mx-auto grey lighten-4" elevation="0">
            <v-slide-group cycle class="pa-4 mx-auto" show-arrows>
                <v-slide-item v-for="(item,i) in items" :key="i" class="text-center">
                    <v-card  class="ma-4" flat :to="`/communities/${getName(item.community_name)}`" style="cursor : pointer;">
                        <v-img :src="item.community_banner" :height="windowSize ? '150' : '300'" :width="windowSize ? '160' : '320'">
                            <p class="mb-0 text-h6 white--text">{{item.community_name}}</p>
                        </v-img>
                    </v-card>
                </v-slide-item>
            </v-slide-group>
        </v-sheet>
    </div>
</template>

<script>

export default {
    
    data(){
        return{
            items:[]
        }
    },
    mounted(){
        this.onload()
    },
    methods:{
        getName(val){
            return val.replace(/\s/g,'-')
        },
        async onload(){
            await this.$axios.$get('communities/all')
            .then(res=>{
                this.items = res
            })
            .catch(e => console.log(e))
        },
    },
    computed:{
        windowSize(){
            return this.$vuetify.breakpoint.mobile ? true : false
        }
    }
}
</script>

<style scoped>
    .searchCard{
        background: rgba(0,0,0,.6);
        padding: 15px 15px 8px;
        border-radius: 5px;
    }
</style>