<template>
    <div
            :class="enable?'btn':'disable-btn'"
    >
        {{buttonText}}
    </div>
</template>

<script>
    export default {
        name: "Button",
        props: ['buttonText','enable'],
    }
</script>

<style>
    .btn{
        width: 100px;
        height: 34px;
        background: #F4E041;
        border-radius: 80px;
        text-align: center;
        font-family: 'Nunito';
        font-style: normal;
        font-weight: 400;
        font-size: 16px;
        line-height: 34px;
        user-select: none;
    }

    .disable-btn{
        width: 100px;
        height: 34px;
        background: #B4B4B4;
        border-radius: 80px;
        text-align: center;
        border-radius: 80px;
        text-align: center;
        font-family: 'Nunito';
        font-style: normal;
        font-weight: 400;
        font-size: 16px;
        line-height: 34px;
        user-select: none;
    }

    .btn:hover,.disable-btn:hover{
        cursor: pointer;
    }
</style>