<template>
  <div class="mt-10 font-bold text-5xl ">
    <h1>Gerenciar Pedidos:</h1>
    <dashboardPedidos />
  </div>
</template>

<script>
import dashboardPedidos from '../components/dashboardPedidos.vue'

export default {
  name:'pedidosView',
  components:{dashboardPedidos}
  
}
</script>
<style scoped>

</style>