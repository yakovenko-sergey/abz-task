<template>
    <div class="preloader__wrapper spinner" v-if="showPreloader"></div>
</template>

<script>
    export default {
        name: "Preloader",
        props:['showPreloader']
    }
</script>

<style>
    .spinner{
        width: 50px;
        height: 50px;
        border: 5px solid #f3f3f3;
        border-top:5px solid #0c9cf3;
        border-radius: 100%;
        position: absolute;
        bottom:200px;
        left:0;
        right: 0;
        margin: auto;
        z-index: 10;
        animation: spin 1s infinite linear;
    }

    @keyframes spin {
        from{
            transform: rotate(0deg);
        }to{
             transform: rotate(360deg);
         }
    }

</style>