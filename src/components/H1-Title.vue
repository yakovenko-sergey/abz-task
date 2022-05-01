<template>
    <h1 class="h1__title">{{title}}</h1>
</template>

<script>
    export default {
        name: "H1-Title",
        props:['title']
    }
</script>

<style>
    .h1__title{
        font-family: 'Nunito';
        font-style: normal;
        font-weight: 400;
        font-size: 40px;
        line-height: 40px;
        display: flex;
        justify-content: center;
        text-align: center;
    }

    @media screen and (min-width:0px){
        .h1__title{
            margin: 140px 30px 0;
        }
    }
</style>