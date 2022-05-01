<template>
    <div class="user__item">
        <img :src="photo">
        <div class="user__name"
             @mouseover="hoverToElem"
             @mouseleave="hoverOutElem"
        >
            {{name}}
        </div>
        <div class="user__info">
            <div class="user__info-item">{{position}}</div>
            <div class="user__info-item user__info-email"
                 @mouseover="hoverToElem"
                 @mouseleave="hoverOutElem"
            >
                {{email}}
            </div>
            <div class="user__info-item">{{phone}}</div>
        </div>
        <vHint
                :hint="hint"
        />
    </div>
</template>

<script>
    import vHint from '../components/Hint'
    export default {
        name: "UserItem",
        components:{
          vHint
        },
        props:['photo','name','position','email','phone'],
        data(){
            return{
                hint:{
                    hintText:'',
                    positionY:0,
                }
            }
        },
        methods:{
           hoverToElem(e){
               this.hint.positionY=e.target.offsetTop;
               this.hint.hintText=e.target.innerText
           },
            hoverOutElem(e){
               this.hint.hintText='';
            }
        }
    }
</script>

<style>
    .user__item{
        display: flex;
        flex-direction: column;
        align-items: center;
        flex-basis: 33%;
        gap: 20px;
        padding: 20px;
        max-width: 330px;
        background: #FFFFFF;
        border-radius: 10px;
        /*overflow: hidden;*/
        position: relative;
    }
    .user__item div {
        text-align: center;
        text-overflow: ellipsis;
        white-space: nowrap;
        overflow: hidden;
        width: 100%;
    }
    .user__item > img{
        width: 70px;
        height: 70px;
        border-radius: 100%;
    }

    .user__info-item{
        padding:3px;
    }
    .user__info{
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
        width: 100%;
    }

    .user__info-email,.user__name:hover{
        cursor: pointer;
    }

    @media only screen and (min-width:0px) {
        .user__item {
            flex-basis: 100%;
        }
    }

    @media only screen and (min-width:768px) {
        .user__item {
            flex-basis: 40%;
          }
    }

    @media only screen and (min-width:1024px) {
        .user__item {
            flex-basis: 24%;
        }
    }

    @media only screen and (min-width:1170px) {
        .user__item {
            flex-basis: 28%;
        }
}
</style>