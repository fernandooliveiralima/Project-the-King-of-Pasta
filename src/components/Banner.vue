<template>
    <div id="main-banner">
        <h1>the king of pasta</h1>
    </div>
</template>

<script>
export default {
    name: 'Banner'
}
</script>

<style scoped>
    #main-banner{
        background-image: url('/public/img/banner.jpg');
        background-position: 0 -250px;
        background-size: cover;
        height: 500px;
        display: flex;
        align-items: center;
        justify-content: center;
        background-repeat: no-repeat;
    }

    h1{
        color: #ee9f07;
        font-size: 62px;
        text-transform: capitalize;
        background-color: #ba322b;
        text-align: center;
        padding: 20px 40px;
    }
</style>