<template>
  <div>
    <b-container>
      <b-row align-h="center">
        <b-input-group style="width: 44rem;">
            <b-form-input class="border" @keyup.enter="filter()" type="text" v-model="search" placeholder="Buscar Promoción">
            </b-form-input>
          <b-input-group-append>
            <b-button @click ="filter()" variant="outline-secondary">Button</b-button>
          </b-input-group-append>
        </b-input-group>
      </b-row>

      <b-row>
        <b-col >
          <b-card-group class="mt-4" columns>
            <Promotion v-for="promo in promotions" :key="promo.id" :promo="promo">
            </Promotion>
          </b-card-group> 
        </b-col>   
      </b-row>

      <p v-if="load & promotions.length == 0" class="text-center mt-5 mb-5">No tiene Promociones</p> 
    </b-container>

   <p class="mt-5" v-if="errors === 500">No se pudo conectar al servidor</p>
  </div>
  

</template>

<script>
import {mapState} from "vuex";
import Promotion from "@/components/Promotion/PromotionComponent.vue";

export default {
   name: 'home',
   data(){
     return{
       search: '',
       load: false
     }
   },
   components: {
    Promotion,
  },
  mounted(){
    this.$store.dispatch('getPromotions').then(()=>{this.load = true});
    this.$store.commit('StudentsList', '')
    },
  methods:{
    filter(){
      this.$store.dispatch('getPromotionsFiltered', this.search);
    }
  },
  computed:{
       ...mapState(['promotions', 'errors']),
        
  }
}
</script>
