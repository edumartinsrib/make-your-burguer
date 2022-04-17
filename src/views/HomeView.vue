<template>
   <div class="">
     <bannerMain />
    <div class="font-bold text-5xl ">
    <h1>Monte o seu próprio Burger personalizado!</h1>
    <burgerForm />
    </div>
  </div>
</template>

<script>
import bannerMain from '../components/bannerMain.vue'
import burgerForm from '../components/burgerForm.vue'

export default {
    name:'HomeView',
    components:{bannerMain, burgerForm}
}
</script>