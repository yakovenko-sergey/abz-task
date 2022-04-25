<template>
    <div class="wrapper__users">
        <div class="users__title mg-block">
            <vH1Title :title="'Working with GET request'"/>
        </div>
        <div class="users__container">
            <vUserItem
                    v-for="user in usersArr['users']"
                    :key="user"
                    :photo="user['photo']"
                    :name="user['name']"
                    :position="user['position']"
                    :email="user['email']"
                    :phone="user['phone']"
            />
        </div>
        <vButton
                class="users__more-btn btn"
                :buttonText="'Show more'"
                :enable="true"
                @click="getUsers(this.usersArr['links']['next_url'])"
                v-if="usersArr['page']<usersArr['total_pages']"
        />
    </div>
</template>

<script>
    import vButton from './Button'
    import vUserItem from '../components/UserItem'
    import vH1Title from '../components/H1-Title'
    export default {
        name: "Users",
        components:{
            vButton,
            vUserItem,
            vH1Title
        },
        props: ['scrollTo','requestGET'],
        data(){
            return{
                usersArr:[]
            }
        },
        mounted(){
            this.getUsers('https://frontend-test-assignment-api.abz.agency/api/v1/users?page=1&count=6');
        },
        methods:{
            getUsers(url){
                this.requestGET(url).
                then(data=>{
                    if (data.users){
                        for (let key in data){
                            if (this.usersArr['users'] && key==='users'){
                                this.usersArr[key]=this.usersArr[key].concat(data[key]);
                                this.scrollToBlock();
                                return;
                            }
                            this.usersArr[key]=data[key];
                        }
                        console.log(this.usersArr);
                    }
                });
            },
            scrollToBlock(){
                let elem=document.querySelector('.users__container');
                let blockHeight=elem.clientHeight;
                this.$nextTick(()=>{
                    let scrollPos=elem.offsetTop+blockHeight;
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
    .users__container{
        display: flex;
        flex-wrap: wrap;
        gap: 29px;
        font-family: 'Nunito';
        font-style: normal;
        font-weight: 400;
        font-size: 16px;
        justify-content: center;
    }
    .users__more-btn{
        width: 120px;
    }

    @media only screen and (min-width:0px) {
        .users__container {
            gap: 20px;
            margin: 0 25px;
        }
        .users__more-btn{
            margin:49px auto 140px;
        }
    }

    @media only screen and (min-width:380px) {
        .users__container {
            gap:27px;
            margin:0;
        }
    }

    @media only screen and (min-width:768px) {
        .users__container {
            gap:15px;
        }
    }

    @media only screen and (min-width:1024px){
        .users__container {
            gap: 25px;
        }
    }

    @media only screen and (min-width:1170px) {
        .users__container {
            gap: 30px;
        }
    }





</style>