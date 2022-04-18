<template>
    <div class="users__item">
        <img :src="photo">
        <div class="users__name">{{name}}</div>
        <div class="users__info">
            <div class="user__info-item">{{position}}</div>
            <div class="user__info-item">{{email}}</div>
            <div class="user__info-item">{{phone}}</div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "UserItem",
        props:['photo','name','position','email','phone']
    }
</script>

<style>
    .users__item{
        display: flex;
        flex-direction: column;
        align-items: center;
        flex:1 1 28%;
        gap: 20px;
        padding: 20px;
        max-width: 370px;
        background: #FFFFFF;
        border-radius: 10px;
        overflow: hidden;
    }
    .users__item div {
        text-align: center;
        text-overflow: ellipsis;
        white-space: nowrap;
        overflow: hidden;
        width: 100%;
    }
    .users__item > img{
        width: 70px;
        height: 70px;
        border-radius: 100%;
    }

    .user__info-item{
        padding:3px;
    }
    .users__info{
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
        width: 100%;
    }
</style>