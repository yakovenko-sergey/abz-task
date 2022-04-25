<template>
    <div class="wrapper__header">
        <div class="header__content">
            <div class="header__title">
                <h1>Test assignment for front-end developer</h1>
                <h2>What defines a good front-end developer is one that has skilled knowledge of HTML, CSS, JS with a vast understanding of User design thinking as they'll be building web interfaces with accessibility in mind. They should also be excited to learn, as the world of Front-End Development keeps evolving.</h2>
                <vButton class="header__signup-btn" :buttonText="'Sign up'" @click="scrollTo('.wrapper__signup')" :enable="true"/>
            </div>
        </div>
    </div>
</template>

<script>
    import vButton from './Button'
    export default {
        name: "Header",
        props: ['scrollTo'],
        components:{
            vButton
        }
    }
</script>

<style>
    .header__content{
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 1170px;
        height: 650px;
        max-width: 100%;
        background: linear-gradient(0deg, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url("../assets/pexels-alexandr-podvalny-1227513.jpg");
    }

    .header__title h1{
        font-family: 'Nunito';
        font-style: normal;
        font-weight: 400;
        font-size: 40px;
        line-height: 40px;
        color: #FFFFFF;
        margin-bottom:21px;
        text-align: center;
    }
    .header__title h2{
        font-family: 'Nunito';
        font-style: normal;
        font-weight: 400;
        font-size: 16px;
        line-height: 26px;
        text-align: center;
        color: #FFFFFF;
        margin-bottom:32px;
    }
    .header__signup-btn{
        margin: auto;
    }

    @media only screen and (min-width:0px) {
        .header__content{
            height: 500px;
        }

        .header__title{
            width: 330px;
            margin: 40px;
        }

    }

    @media only screen and (min-width:380px) {
        .header__title{
            width: 380px;
        }
        .header__content{
            justify-content: center;
        }
    }

    @media only screen and (min-width:1024px) {
        .header__content{
            height: 650px;
        }
    }

</style>