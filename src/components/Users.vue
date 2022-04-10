<template>
    <div class="wrapper__users">
        <div class="users__title mg-block">       <!-- Change class -->
            <h1>Working with GET request</h1>
        </div>
        <div class="users__container">
            <div class="users__item"
                 v-for="user in usersArr['users']" :key="user">
                <img :src="user['photo']">
                <div class="users__name">{{user['name']}}</div>
                <div class="users__info">
                    <div class="user__info-item">{{user['position']}}</div>
                    <div class="user__info-item">{{user['email']}}</div>
                    <div class="user__info-item">{{user['phone']}}</div>
                </div>
            </div>
        </div>
        <div class="users__more-btn btn"
             @click="this.getUsers(this.usersArr['links']['next_url'])"
             v-if="this.usersArr['page']<this.usersArr['total_pages']">
            Show more
        </div>
    </div>
</template>

<script>
    export default {
        name: "Users",
        data(){
            return{
                usersArr:[],
                blockHeight:0
            }
        },
        mounted(){
       //     this.getUsers('https://frontend-test-assignment-api.abz.agency/api/v1/users?page=1&count=6');
        },
        methods:{
            getUsers(url){
                fetch(url)
                    .then((response) => {
                        return response.json();
                    })
                    .then((data) => {
                        for (let key in data){
                            if (this.usersArr['users'] && key==='users'){
                                this.usersArr[key]=this.usersArr[key].concat(data[key]);
                                this.scrollToBlock();
                                return;
                            }
                                this.usersArr[key]=data[key];
                        }
                     })
                    .catch(ex=>{
                        console.log('parsing failed', ex)
                    });
                console.log(this.usersArr);
            },
            scrollToBlock(){
                let elem=document.querySelector('.users__container');
                this.blockHeight=elem.clientHeight;
                this.$nextTick(()=>{
                    let scrollPos=elem.offsetTop+this.blockHeight;
                    window.scrollTo({
                        top:scrollPos,
                        behavior:'smooth'
                    })
                });
            }
        }
    }
</script>

<style>
    .mg-block{
        margin: 140px 0 50px 0;
    }
    .users__title h1{
        font-family: 'Nunito';
        font-style: normal;
        font-weight: 400;
        font-size: 40px;
        line-height: 40px;
        display: flex;
        justify-content: center;
    }
    .users__container{
        display: flex;
        flex-wrap: wrap;
        gap: 29px;
        font-family: 'Nunito';
        font-style: normal;
        font-weight: 400;
        font-size: 16px;
    }
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
    .users__more-btn{
        margin:49px auto 0;
        width: 120px;
    }
</style>