<template>
    <div class="success__wrapper">
        <div class="success__message">{{Message}}</div>
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
    }

</style>