<template>
    <div class="wrapper__logo-menu">
        <div class="menu__container">
            <div class="logo">
                <img src="../assets/Logo.svg">
            </div>
            <nav class="menu">
                <div class="menu__item btn">Users</div>
                <div class="menu__item btn">Sign up</div>
            </nav>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Menu"
    }
</script>

<style>
    .wrapper__logo-menu{
        background: #fff;
    }
    .menu__container{
        max-width: 1170px;
        display: flex;
        align-items: center;
        justify-content: flex-start;
        height: 60px;
        margin: auto;
    }

    .menu{
        display: flex;
        justify-content: flex-end;
        flex: 1;
    }
    .menu__item{
        margin: 0 0 0 10px;
    }
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
    }

    .btn:hover,.disable-btn:hover{
        cursor: pointer;
    }
</style>