<template>
    <div class="bg-slate-100  min-w-max">
      <div class="flex items-center text-center justify-between p-3">
        <h1 class="font-bold text-base py-6 pl-10">Liste des dossiers</h1>
        <button class="bg-cyan-700 w-70 h-9 p-5  text-white rounded-lg flex items-center justify-between" @click="showModal = !showModal">
      <img src="../assets/add.svg" class="bg-white w-5 h-5 rounded-3xl m-3">
           
      Ajouter un dossier</button>
  <div class="absolute  justify-center items-center">
  
      <ModalAjouterDossier :show="showModal" @close="showModal = false">
           <AjouterDossier />
      </ModalAjouterDossier>
  </div>
      </div>
    <div class="bg-white px-10 rounded-xl">
        <btnmagic/>
                              <!-- ChercheBar -->
                       <chercheBar/>
                          <!-- Tableau de suive -->
                  <div class="overflow-hidden  border-inherit rounded-lg">
                      <table class="min-w-full divide-y  divide-gray-100">
                          <thead class="bg-cyan-700  ">
                              <tr  class="border-2" >
                                  <th scope="col" class="py-3 pl-4 border-2 rounded-tl-md">
                                  </th>
                                  <th
                                      scope="col"
                                      class="px-6 py-3 text-xs font-bold text-center border-2 text-[#ffffff] uppercase"
                                  >
                                      Numéro dossier
                                     
                                  </th>
                                <th
                                      scope="col"
                                      class="px-6 py-3 text-xs font-bold text-center border-2 text-[#ffffff] uppercase"
                                  >
                                      Nom Dossier
                                      
   
                                  </th>                             
                                 
                                
                                  <th
                                      scope="col"
                                      class="px-6 py-3 text-xs font-bold text-center border-2 text-[#ffffff] uppercase"
                                  >
                                      Date
                                     
                                  </th>
                                  <th
                                      scope="col"
                                      class="px-6 py-3 text-xs font-bold text-center border-2 text-[#ffffff] uppercase"
                                  >
                                      Statut
                                     
                                  </th>
                                  <th
                                      scope="col"
                                      class="px-6 py-3 text-xs font-bold text-center border-2 rounded-tr-md text-[#ffffff] uppercase"
                                  >
                                      Description
                                  </th>
                                  <td class="px-6 py-3 text-xs font-bold text-center border-2 rounded-tr-md text-[#ffffff] uppercase">
                                      <div class="flex items-center justify-center h-5 ">            
                                        Action                       
                                      </div>
                                  </td>
                              </tr>
                          </thead>
                        
                          <tbody class=" divide-black text-center border-2 border-slate-100 "  
                         >
                              <tr v-for="(item , index) in dossiers" v-bind:key="item" class=" hover:bg-slate-200"  >
                                  <td class="py-3">
                                      <div class="flex items-center justify-center h-5 ">
                                          <input
                                              type="checkbox"
                                              class="text-blue-600  border-gray-200 rounded focus:ring-blue-500"
                                          />                                       
                                      </div>
                                  </td>
                                  <td
                                      class="px-6 py-4 text-sm font-medium text-gray-800 border-2 border-slate-100 whitespace-nowrap  cursor-pointer"
                                      @click="() => NavigationTodevis(item.id)"
                                 > 
                                    {{index+=1}}
                                  </td>
                                  <td
                                      class="px-6 py-4 text-sm font-medium border-2 border-slate-100 text-gray-800 whitespace-nowrap  cursor-pointer"
                                      @click="() => NavigationTodevis(item.id)" >  
  
                                  
                                    {{item.first_name}} {{item.last_name}}
  
                                  </td>
                                 
                                  <td
                                      class="px-6 py-4 text-sm font-medium border-2 border-slate-100 whitespace-nowrap  cursor-pointer"
                                      @click="() => NavigationTodevis(item.id)" >   
                                      {{dateTime(item.date_creation)}}
                                    
                                  </td>
                                  <td
                                  class="px-6 py-4 text-sm font-medium border-2 border-slate-100 whitespace-nowrap  cursor-pointer"
                                  @click="() => NavigationTodevis(item.id)" >  
                                  
                                  {{item.status}}
                                 
                                  </td>
                                  <td
                                  class="px-6 py-4 text-sm font-medium border-2 border-slate-100 whitespace-nowrap  cursor-pointer"
  
                                  >  {{item.description}}
                                      
                                  </td>
                                  <td class=" py-4 text-sm font-medium border-2 border-slate-100 whitespace-nowrap  cursor-pointer">
                                      <div class="flex items-center justify-center h-5 ">
                                        <td class="py-3 px-3">
                                          <div class="flex items-around justify-around h-5  ">
                                           <font-awesome-icon icon="fa-solid fa-pen"  class="  px-2 text-gray-500" />
                                           <font-awesome-icon icon="fa-solid fa-trash"  class=" px-2 text-red-500"  @click="()=> deleteDossier(item.id)"/>

                                      </div>
                                       </td>                                      
                                      </div>
                                  </td>
                              </tr>
                             </tbody>
                          </table>
                      </div>
                     </div>
                   </div>
  </template>



<script>
import chercheBar from "../screen/chercheBar.vue"
import { ref ,onMounted} from 'vue';
import AjouterDossier from '../components/AjouterUnDossier.vue'
import  ModalAjouterDossier from "../components/ModelAjouterUnDossier.vue"
import axios from 'axios'
import { useRouter} from "vue-router"
import { mapActions, mapGetters, mapMutations } from 'vuex'
import moment from 'moment'
import Swal from 'sweetalert2'


export default {
name:"Accueil",

data()
{
    return {
       router:useRouter(),
       showModal:false,
       ShowProfil: false,
       show : false ,
       deconnection : false ,
    
    }
},


props :{
    show: {
    type: Boolean,
    default: false,
  },
  },
  components: {
    chercheBar ,
    AjouterDossier ,
    ModalAjouterDossier,
    
  },
  computed : {
     ...mapGetters(['dossiers']),
         },
         

  methods: {
    deleteDossier(el_Id){
        Swal.fire({
        title: 'Vous etes sur ?',
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#0E7490',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Oui supprimer!'
  }).then((result) => {
    if (result.isConfirmed) {
      axios.delete("/api/dossiers/",{params: { 
                    dossier_id : el_Id
                } }).then(response=>{
                  Swal.fire(
                    'Supprimé!',
                    'le document est supprimé.',
                    'success'
                  )
                
                }).then(res=>{
                    window.location.reload()
                })
            }
  })  
 },

    dateTime(value) {
      return moment(value).format("DD-MM-YYYY [à] HH:mm a");
    },
    
    ...mapActions(['getdossiers']),
   async NavigationTodevis (id) {
        console.log('id_Navigation',id)     
        this.router.push({
            path : '/Pochettes/1',
            query : { id_dossier : id }
            
        })

     }  
  },

  async mounted  () {
   const response = await this.getdossiers()
 }
}
 </script>
<style scoped>
@media only screen and (min-width: 320px) and (max-width: 480px) {
    /* ruleset for 320px - 480px */
}
@media only screen and (min-width: 768px) and (max-width: 1024px) and (orientation: landscape) {
    /* regles CSS */
}
</style>