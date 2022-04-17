<template>
    <div id="main-Banner" class="bg-center">
        <h1 class="text-white bg-gradient-to-r border-r-5 from-blue-500 text-6xl ">Faça seu Hamburguer!</h1>
    </div>
</template>

<script>
export default {
    name:'bannerMain'    
}
</script>
<style scoped>

#main-Banner{
    background-image: url('../../public/img/burger.jpg');
    background-position: 0 -250px;
    background-size: cover;
    height: 700px;
    display: flex;
    width: 100%;
    align-items: center;
    justify-content: left;
}
</style>