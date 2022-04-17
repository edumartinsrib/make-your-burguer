<template>
    <div role="alert">
        {{msg}}
    </div>
</template>
<script>
export default {
    name: 'MessageError',
    props: {
        msg: String,
    }
}
</script>

<style scoped>
.message-container{
    width: 400px;
    margin: 30px auto;
}
</style>