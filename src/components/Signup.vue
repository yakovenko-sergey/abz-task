<template>
    <div class="wrapper__signup">
        <div v-if="!successReg" class="signup__before-success">
            <div class="signup__title">
                <vH1Title :title="'Working with POST request'"/>
            </div>
            <form class="singup__form" action="#" method="post">
                <div class="signup__container">
                    <div class="signup__input-container">
                        <p class="signup__error error">{{errFromServer}}</p>
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
        </div>
        <vSuccessBlock
                v-if="successReg"
                :Message="'User successfully registered'"
        />
    </div>
</template>

<script>
    import vInput from '../components/Inputs'
    import vInputFile from '../components/InputsFile'
    import vInputRadio from '../components/InputsRadio'
    import vButton from './Button'
    import vSuccessBlock from '../components/SuccessBlock'
    import vH1Title from '../components/H1-Title'
    export default {
        name: "Signup",
        props:['requestToApi','users'],
        components:{
            vInput,
            vInputFile,
            vInputRadio,
            vButton,
            vSuccessBlock,
            vH1Title
        },
        data(){
            return{
                inputs:[],
                inputChecked:false,
                positions:[],
                successReg:false,
                errFromServer:''
            }
        },
        mounted(){
            this.requestToApi('https://frontend-test-assignment-api.abz.agency/api/v1/positions').
            then(data=>{
                if (data.positions) this.positions=data.positions;
            });
        },
        methods:{
            inputUpdate(data){
                console.log(data);
                for (let key in this.inputs){
                    if (!this.inputs[key].validation){
                        this.inputChecked=false;
                        break;
                    }
                    this.inputChecked=true;
                }
            },
            addNewUser(){
               this.requestToApi('https://frontend-test-assignment-api.abz.agency/api/v1/token').
               then(data=>{
                       if(data.token) {
                            return data.token;
                       }
               }).
                   then(token=>{
                       let formData = new FormData();
                       let inputs=this.inputs;
                       for (let key in this.inputs){
                           key=='phone' ?
                            formData.append(this.inputs[key].alias, this.inputs[key].val.replace(/[^\d\\+]/g, '')) :
                            formData.append(this.inputs[key].alias, this.inputs[key].val)
                       }
                   const config={
                       method: 'POST',
                       body: formData,
                       headers:
                           { 'Token': token}
                   }
                   this.requestToApi('https://frontend-test-assignment-api.abz.agency/api/v1/users',config).
                   then(data=>{
                       console.log(data);
                       if (data.success){
                           this.$emit('renewUsers');
                           this.successReg=true;
                       }
                       else if(data.fails){
                           let reg=new RegExp(/[\w \s \\.]+/);
                            for (let key in data.fails){
                                this.inputs[key].validation=false;
                                this.inputs[key].errorText=reg.exec(data.fails[key])[0];
                            }
                       }
                       else{
                           this.inputs['email'].validation=false;
                           this.inputs['phone'].validation=false;
                           this.errFromServer=data.message;
                       }
                   }).catch(e=>console.log('Error',e))
               });
            },
            failForm(){
                for (let key in this.inputs){
                    this.inputs[key].changeFlag=true;
                }
            }
        }
    }
</script>

<style>
    .mg-block{
        margin: 140px 0 50px 0;
    }

    .signup__container{
        max-width: 380px;
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

    .signup__error{
        color:red;
        font-size: 16px;
    }

    @media only screen and (min-width: 0px){
        .signup__container{
            margin: 0 20px 140px;
        }
    }

    @media only screen and (min-width: 380px){
        .signup__container{
            margin: 0 auto 140px;
        }
    }


    @media only screen and (min-width: 768px){
        .signup__title{
            margin:140px 0 0;
        }

        .input__wrapper input{
            font-size: 15px;
        }

        .input-file__label{
            line-height: 50px;
            margin:37px 0 0;
        }

        .signup__submit-btn{
            margin: 50px auto 0;
        }
    }
</style>