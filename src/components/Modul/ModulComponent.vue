<template>
    <div>
          <b-card class="ml-2" @click="selectModul"
            header="Modul"
            :border-variant="color"
            header-text-variant="white"
            header-tag="header"
            :header-bg-variant="color"
            :sub-title="modul.name"
            sub-title-text-variant ="normal"
            style="width: 8rem; height:8.3rem"
            >
            <b-card-text>
            {{color == 'danger' ? 'Incompleto' : 'Completo'}} 
            </b-card-text>

          </b-card>
    </div>
</template>
<script>
export default {
    props: ['modul'],
    methods: {
      selectModul(){
        this.$store.commit('ModulSelected', this.modul)
        this.$router.push({name: 'modul.detail' , params:{ 
          modul:this.modul.name.replace(' ', '')}
          })
      }
    },
    computed:{
      color(){
        if(this.modul.informe == null|| this.modul.memorandum == null || this.modul.solicitud == null|| this.modul.proyecto == '0'|| this.modul.f_supervision == '0'||this.modul.f_evaluacion == null||this.modul.recibo == '0'){
          return 'danger'      
        }else{
        return 'primary'
      }
     }
   } 
}
</script>