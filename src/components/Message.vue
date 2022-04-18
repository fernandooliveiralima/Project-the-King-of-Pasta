<template>
    <div class="message-container">
        <p> {{ msg }} {{ id }} </p>
    </div>
</template>

<script>
export default {
    name: 'Message',
    props:{
        msg: String,
        id: String
    }
}
</script>

<style scoped>
    .message-container{
        background-color: #b8f493;
        color: #196c19;
        border: 2px solid #5ab55a;
        border-radius: 4px;
        padding: 10px;
        max-width: 400px;
        margin: 30 auto;
        text-align: center;
        margin-left: 400px;
        margin-bottom: 20px;
    }
</style>