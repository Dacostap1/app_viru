<template>
    <div>
        
    </div>
</template>
<script>
export default {

    created(){
        this.$store.commit('NuevoToken', ''),
        localStorage.removeItem('token'),
        this.$router.push({name: 'login'})
        this.$store.commit('PromotionsList', []); //limpiar las promociones por si se logea otro usuario despues
       this.$store.commit('OptionSelected', null);
       this.$store.commit('errorsList', []);
    }
    
}
</script>