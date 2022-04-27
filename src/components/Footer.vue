<template>
    <div class="footer__wrapper">
        <div class="footer__container">
            <p>© abz.agency specially for the test task</p>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Footer"
    }
</script>

<style>
    .footer__wrapper{
        font-family: 'Nunito';
        font-style: normal;
        font-weight: 400;
        font-size: 16px;
        line-height: 26px;
        background: #fff;
    }

    .footer__container{
        display: flex;
        max-width: 1170px;
        margin: 0 auto;
        padding-left: 50px;
        align-items: center;
        height: 60px;

    }
</style>