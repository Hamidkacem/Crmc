<template >
  <div class="bg-slate-100  px-5 rounded">   
    <section class="bg-white h-full rounded-lg">
      <section class="w-full">
        <div class="py-3 text-left   ">
                      <!-- Second Div -->
                      <div class="border-b-2 p-2">
                      <div class="flex flex-row  justify-end  px-24 ">
                        <div class="absolute left-40 py-4  ">
                          <span class=" text-left font-bold text-lg  ">{{title}}</span>
                        </div>
                            <a :href="'http://192.168.1.36:8000'+pochette.url_pdf" target="_blank">
                              
                              <button  class="bg-cyan-700  w-32 h-10 rounded-md text-xs mr-4 text-white">
                                     Voir PDF
                             <font-awesome-icon icon="fa-solid fa-eye" color="" class="ml-2" />
                            </button> 

                            </a>
                           
                        <div v-if="Modifer"  @click="Modifer = !Modifer" >
                           <button class="bg-cyan-700 w-32 h-10 rounded text-xs mr-4  text-white"> Modifier
                             <font-awesome-icon icon="fa-solid fa-pen"  class="ml-2"/>
                            </button>
                            
                          </div>

                          <div v-if="!Modifer"  @click="Modifer = !Modifer">
                            
                            <button class="bg-cyan-700 w-32 h-10 rounded text-xs  text-white"> Enregister
                              <font-awesome-icon icon="fa-solid fa-check"  class="ml-2"/>
                            </button>
                          </div>

                          <div>
                            <button :class='[Modifer ? "bg-red-500 w-32 h-10 rounded text-xs  text-white" : "bg-slate-500 w-32 h-10 rounded text-xs  text-white ml-4"]' @click="deletePochette" > 
                              Supprimer
                              <font-awesome-icon icon="fa-solid fa-trash"  class="ml-2"/>
                            </button>
                          </div>
                        </div>
                      </div>
                        </div>
                    
                    </section>
                  
            <section class="flex flex-col justify-center items-center  text-white text-center py-10" v-if='id_props_pochette != 1 & id_props_pochette !=5 '>
                      <div class="flex flex-row py-1 " v-if="pochette.nom_client">
                          <h1 class="border rounded-l-md border-slate-400 py-3 w-36  text-xs font-bold	bg-cyan-600">Nom Client</h1>
                          <input :class='[Modifer ? "border rounded-r-md border-slate-400 bg-slate-100  flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2" : "border rounded-r-md border-slate-400 bg-white flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2"]'  :value="pochette.nom_client ? pochette.nom_client : 'null' "  :disabled="this.Modifer"/>
                      </div>
                      <div class="flex flex-row py-1" v-if="pochette.gain_energetique">
                        <h1 class="border rounded-l-md border-slate-400 py-3 w-36  text-xs font-bold	bg-cyan-600">Gain Energetique</h1>
                        <input :class='[Modifer ? "border rounded-r-md border-slate-400 bg-slate-100  flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2" : "border rounded-r-md border-slate-400 bg-white flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2"]'  :value='pochette.gain_energetique' :disabled="this.Modifer"/>
                      </div>
                      <div class="flex flex-row py-1" v-if="pochette.cef_projet">
                         <h1 class="border rounded-l-md border-slate-400 py-3 w-36  text-xs  font-bold	bg-cyan-600">Cef Projet /Cep Projet </h1>
                         <input :class='[Modifer ? "border rounded-r-md border-slate-400 bg-slate-100  flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2" : "border rounded-r-md border-slate-400 bg-white flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2"]'  :value='pochette.cef_projet+" / " +pochette.cep_projet' :disabled="this.Modifer" />
                      </div>
                    <div class="flex flex-row py-1" v-if="pochette.cef_init && pochette.cep_init">
                      <h1 class="border rounded-l-md border-slate-400 py-3 w-36  text-xs font-bold	bg-cyan-600">Cef Initiale / Cep Initiale</h1>
                      <input :class='[Modifer ? "border rounded-r-md border-slate-400 bg-slate-100  flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2" : "border rounded-r-md border-slate-400 bg-white flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2"]'   :value='pochette.cef_init + " / "+ pochette.cep_init' :disabled="this.Modifer"/>
                    </div>
                     <!-- date_visite -->
                    <div class="flex flex-row py-1" v-if="pochette.date_visite">
                      <h1 class="border rounded-l-md border-slate-400 py-3 w-36  text-xs font-bold	bg-cyan-600">Date de visite</h1>
                     <input :class='[Modifer ? "border rounded-r-md border-slate-400 bg-slate-100  flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2" : "border rounded-r-md border-slate-400 bg-white flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2"]'   :value='pochette.date_visite' :disabled="this.Modifer"/>
                    </div>
                    <!-- adresse_email -->
                  <div class="flex flex-row py-1" v-if="pochette.adresse_email">
                   <h1 class="border rounded-l-md border-slate-400 py-3 w-36 text-center text-xs font-bold	bg-cyan-600">Adresse Email</h1>
                   <input :class='[Modifer ? "border rounded-r-md border-slate-400 bg-slate-100  flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2" : "border rounded-r-md border-slate-400 bg-white flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2"]'   :value='pochette.adresse_email' :disabled="this.Modifer"/>
                  </div>
                  <!-- date_cette_proposition -->
                  <div class="flex flex-row py-1" v-if="pochette.date_cette_proposition">
                    <h1 class="border rounded-l-md border-slate-400 py-3 w-36 text-center text-xs  font-bold	bg-cyan-600">Date de cette proposition</h1>
                   <input :class='[Modifer ? "border rounded-r-md border-slate-400 bg-slate-100  flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2" : "border rounded-r-md border-slate-400 bg-white flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2"]'   :value='pochette.date_cette_proposition' :disabled="this.Modifer"/>
                 </div>
                 <!-- ref_audit -->
                 <div class="flex flex-row py-1" v-if="pochette.ref_audit">
                    <h1 class="border rounded-l-md border-slate-400 py-3 w-36 text-center text-xs  font-bold	bg-cyan-600">Ref Audit</h1>
                   <input :class='[Modifer ? "border rounded-r-md border-slate-400 bg-slate-100  flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2" : "border rounded-r-md border-slate-400 bg-white flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2"]'   :value='pochette.ref_audit' :disabled="this.Modifer"/>
                 </div>
              <div class="flex flex-row py-1 " v-if="id_props_pochette == 3">
                <h1 class="border rounded-l-md border-slate-400 py-3 w-36 text-xs font-bold text-center 	bg-cyan-600">Montant de prime
                </h1>
                <input :class='[Modifer ? "border rounded-r-md border-slate-400 bg-slate-100  flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2" : "border rounded-r-md border-slate-400 bg-white flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2"]'  :value='pochette.montant_prime ? pochette.montant_prime : "Null" ' :disabled="this.Modifer"/>
             </div>
             <div class="flex flex-row py-1 " v-if="pochette.parcelle_cadastrale">
                <h1 class="border rounded-l-md border-slate-400 py-3 w-36  text-xs font-bold	bg-cyan-600">Parecelle Cadastrale</h1>
                <input :class='[Modifer ? "border rounded-r-md border-slate-400 bg-slate-100  flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2" : "border rounded-r-md border-slate-400 bg-white flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2"]'  :value="pochette.parcelle_cadastrale ? pochette.parcelle_cadastrale : 'null' "  :disabled="this.Modifer"/>
             </div>
             <div class="flex flex-row py-1 " v-if="pochette.adresse_client">
                <h1 class="border rounded-l-md border-slate-400 py-3 w-36  text-xs font-bold	bg-cyan-600">Adresse Client</h1>
                <input :class='[Modifer ? "border rounded-r-md border-slate-400 bg-slate-100  flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2" : "border rounded-r-md border-slate-400 bg-white flex-row  w-[550px] ml-1 text-xs  py-2 text-black text-left p-2"]'  :value="pochette.adresse_client ? pochette.adresse_client : 'null' "  :disabled="this.Modifer"/>
             </div>
              
        </section> 
        <section  class="py-4 " v-if="id_props_pochette === 1 || id_props_pochette === 5">
                      <div class="flex flex-center justify-center items-center">
                       <div  class="text-white border-separate border-spacing-1 flex flex-col item-center text-center justify-center">
                        <div class="flex flex-row justify-center w-full ">
                                   <!-- TABLE 1  -->
                         <identitéTable :Modifer='Modifer'/>
                                   <!-- TABLE 2 -->
                         <DonneésEnergétiqueTable :Modifer='Modifer'/>
                           </div>
                                  <!-- TABlEAUX 3 -->
                          <TravauxTable :Modifer='Modifer'/>
                                 <!-- Tableaux 4 -->
                          <div class="flex flex-end justify-end">
                            <Montants :Modifer='Modifer'/>
                          </div>                               
                       </div>
                         </div>
                    </section>

        <!-- :class='[this.Modifer ?"border  border-slate-200 py-2 w-52 text-xs text-gray-600 font-bold text-center	bg-slate-100" : "border  border-slate-200 py-2 w-52 text-xs text-gray-600 font-bold text-center	bg-white"]' -->
      </section>
   </div>
   </template>


<script>
import {mapGetters} from 'vuex'
import identitéTable from '../components/pochette/identitéTable.vue'
import DonneésEnergétiqueTable from "../components/pochette/DonneésEnergétiqueTable.vue"
import TravauxTable from "../components/pochette/TravauxTable.vue"
import Montants from "../components/pochette/Montants.vue"
import Swal from 'sweetalert2'
import axios from "axios"
export default {
  name:'DescriptionDevis',
  props:["title"],
  data(){
    return {
      Modifer : true ,
     }

  },
  props : ['id_props_pochette' ,'id_props_dossier',"title" ],  

  components : {
    identitéTable ,
    DonneésEnergétiqueTable ,
    TravauxTable ,
    Montants
  },
  computed : {
     ...mapGetters(['pochette']),
     
  },
  methods: {
    deletePochette(){
  this.Modifer ? (
        Swal.fire({
        title: 'Vous etes sur ?',
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#0E7490',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Oui supprimer!'
  }).then((result) => {
    if (result.isConfirmed) {
      axios.delete("/api/dossiers/document/",{params: {
                    pochette_id : this.id_props_pochette, 
                    dossier_id : this.id_props_dossier ,
                } }).then(response=>{
                  Swal.fire(
                    'Supprimé!',
                    'le document a été supprimé.',  
                  )        
                  this.$emit('onReloadEnd')
                })}
  })
  
  ) : null
      
    },
    }

}
</script>
