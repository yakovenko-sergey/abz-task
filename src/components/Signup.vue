<template>
    <div class="wrapper__signup">
        <div class="signup__title mg-block">
            <h1>Working with POST request</h1>
        </div>
        <form class="singup__form" action="#" method="post">
            <div class="signup__container">
                <div class="signup__input-container">
                    <vInput
                            :inputType="'text'"
                            :inputProp="'name'"
                            :inputPlaceholder="'Your name'"
                            :inputsChild="inputs"
                            @inputUpdate="inputUpdate"
                    />
                    <vInput
                            :inputType="'text'"
                            :inputProp="'email'"
                            :inputPlaceholder="'Email'"
                            :inputsChild="inputs"
                            @inputUpdate="inputUpdate"
                    />
                    <vInput
                            :inputType="'tel'"
                            :inputProp="'phone'"
                            :inputPlaceholder="'Phone'"
                            :inputsChild="inputs"
                            @inputUpdate="inputUpdate"
                    />
                </div>
                <div class="signup__position-container">
                    <div class="signup__position-title">Select your position</div>
                    <vInputRadio
                            :inputsChild="inputs"
                            @inputUpdate="inputUpdate"
                            :items="positions"
                            :groupName="'group1'"
                    />
                </div>
                    <vInputFile
                            :inputsChild="inputs"
                            :id="'file_1'"
                            @inputUpdate="inputUpdate"
                    />
                    <vButton
                            class="signup__submit-btn"
                            :buttonText="'Sign up'"
                            @click="inputChecked?addNewUser():failForm()"
                            :enable="inputChecked"
                    />
            </div>
        </form>
        <vSuccessBlock :Message="'User successfully registered'"/>
    </div>
</template>

<script>
    import vInput from '../components/Inputs'
    import vInputFile from '../components/InputsFile'
    import vInputRadio from '../components/InputsRadio'
    import vButton from './Button'
    import vSuccessBlock from '../components/SuccessBlock'
    export default {
        name: "Signup",
        props:['requestGET','requestPOST','users'],
        components:{
            vInput,
            vInputFile,
            vInputRadio,
            vButton,
            vSuccessBlock
        },
        data(){
            return{
                inputs:[],
                inputChecked:false,
                positions:[],
                successNewUser:{}
            }
        },
        mounted(){
            this.requestGET('https://frontend-test-assignment-api.abz.agency/api/v1/positions').
            then(data=>{
                if (data.positions) this.positions=data.positions;
            });
        },
        methods:{
            inputUpdate(data){
                console.log(this.inputs);
                for (let i=0;i<this.inputs.length;i++){
                    if (!this.inputs[i].validation){
                        this.inputChecked=false;
                        break;
                    }
                    this.inputChecked=true;
                }
            },
            addNewUser(){
               let token;
               this.requestGET('https://frontend-test-assignment-api.abz.agency/api/v1/token').
               then(data=>{
                       if(data.token) {
                            return data.token;
                       }
               }).
                   then(token=>{
                       let formData = new FormData();
                       let inputs=this.inputs;
                       for (let i=0; i<inputs.length;i++){
                           formData.append(inputs[i].alias,inputs[i].val)
                       }
                   const config={
                       method: 'POST',
                       body: formData,
                       headers:
                           { 'Token': token}
                   }
                   this.requestPOST('https://frontend-test-assignment-api.abz.agency/api/v1/users',config).
                   then(data=>{
                       this.successNewUser=data;
                       if (data.success){
                           this.$emit('renewUsers');
                       }
                       else{
                           console.log(this.inputs);
                           console.log(data.fails);
                       }
                   }).catch(e=>console.log('Error',e))
               });
            },
            failForm(){
                for (let i=0;i<this.inputs.length;i++){
                    this.inputs[i].changeFlag=true;
                }
            }
           // var formData = new FormData();
            // file from input type='file'
            // var fileField = document.querySelector('input[type="file"]');
            // formData.append('position_id', 2);
            // formData.append('name', 'Jhon');
            // formData.append('email', 'Jhon@gmail.com');
            // formData.append('phone', '+380955388485');
            // formData.append('photo', fileField.files[0]);
   // fetch('https://frontend-test-assignment-api.abz.agency/api/v1/users',
            // { method: 'POST',
            // body: formData,
            // headers:
            // { 'Token': token, // get token with GET api/v1/token method }, })
            // .then(function(response) { return response.json(); })
            // .then(function(data) { console.log(data);
            // if(data.success) { // process success response }
            // else { // proccess server errors } })
            // .catch(function(error) {
            // proccess network errors });
        }
    }
</script>

<style>
    .mg-block{
        margin: 140px 0 50px 0;
    }
    .signup__title h1{
        font-family: 'Nunito';
        font-style: normal;
        font-weight: 400;
        font-size: 40px;
        line-height: 40px;
        display: flex;
        justify-content: center;
    }

    .signup__container{
        max-width: 380px;
        margin:0 auto 140px;
        font-family: 'Nunito';
        font-style: normal;
        font-weight: 400;
    }

    .signup__input-container{
        display: flex;
        flex-direction: column;
        align-items: center;
        font-size: 16px;
        gap:50px;
    }

    .signup__position-container{
        padding: 28px 0 0;
        font-size: 16px;
    }

    .signup__position-title{
        padding: 0 0 15px;
    }

    .signup__submit-btn{
        display: flex;
        justify-content: center;
        margin: 46px auto 0;
    }
</style>