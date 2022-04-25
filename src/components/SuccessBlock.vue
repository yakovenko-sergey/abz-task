<template>
    <div class="success__wrapper mg-block">
        <h1 class="success__message">{{Message}}</h1>
        <div>
            <img src="../assets/success-image.svg"/>
        </div>
    </div>
</template>

<script>
    export default {
        name: "SuccessBlock",
        props:['Message']
    }
</script>

<style>
    .success__wrapper{
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 50px;
        margin:0 auto 140px;
    }

    .success__wrapper h1{
        font-family: 'Nunito';
        font-style: normal;
        font-weight: 400;
        font-size: 40px;
        line-height: 40px;
    }

</style>