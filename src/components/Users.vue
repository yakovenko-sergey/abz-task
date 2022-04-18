<template>
    <div class="wrapper__users">
        <div class="users__title mg-block">
            <h1>Working with GET request</h1>
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
    export default {
        name: "Users",
        components:{
          vButton,
          vUserItem
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
    .users__more-btn{
        margin:49px auto 0;
        width: 120px;
    }
</style>