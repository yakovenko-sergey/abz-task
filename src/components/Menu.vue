<template>
    <div class="wrapper__logo-menu">
        <div class="menu__container">
            <div class="logo">
                <img src="../assets/Logo.svg" width="104" height="26">
            </div>
            <nav class="menu">
                <vButton :buttonText="'Users'" @click="scrollTo('.wrapper__users')" :enable="true"/>
                <vButton :buttonText="'Sign up'" @click="scrollTo('.wrapper__signup')" :enable="true"/>
            </nav>
        </div>
    </div>
</template>

<script>
    import vButton from './Button'
    export default {
        name: "Menu",
        props: ['scrollTo'],
        components:{
            vButton
        }
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
        height: 60px;
        margin: auto;
    }
    .menu{
        display: flex;
        justify-content: flex-end;
        flex: 1;
    }
    .menu div{
        margin: 0 0 0 10px;
    }

    @media only screen and (min-width:0px){
        .menu__container {
            padding: 0 16px;
            justify-content: center;
        }
    }

    @media only screen and (min-width:380px){
        .menu__container {
            padding: 0 32px;
            justify-content: flex-start;
        }
    }

    @media only screen and (min-width:1024px) {
        .menu__container{
            padding: 0 60px;
        }
    }

</style>