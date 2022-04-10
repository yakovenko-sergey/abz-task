<template>
    <div class="wrapper__signup">
        <div class="signup__title mg-block">
            <h1>Working with POST request</h1>
        </div>
        <form class="singup__form" action="#" method="post">
            <div class="signup__container">
                <div class="signup__input-container">
                    <vInput :inputType="'text'" :inputProp="'name'" :inputsChild="inputs" @inputUpdate="inputUpdate"/>
                    <vInput :inputType="'text'" :inputProp="'email'" :inputsChild="inputs" @inputUpdate="inputUpdate"/>
                    <vInput :inputType="'tel'" :inputProp="'phone'" :inputsChild="inputs" @inputUpdate="inputUpdate"/>
                </div>
                <div class="signup__position-container">
                    <div class="signup__position-title">Select your position</div>
                    <vInputRadio/>
                </div>
                        <vInputFile
                                :inputsChild="inputs"
                                @inputUpdate="inputUpdate"
                        />
                        <button class="signup__submit-btn" :class="inputChecked?'btn':'disable-btn'"
                             @click.prevent="inputsValidate">
                            Sign up
                        </button>

            </div>
        </form>
    </div>
</template>

<script>
    import vInput from '../components/Inputs'
    import vInputFile from '../components/InputsFile'
    import vInputRadio from '../components/InputsRadio'
    export default {
        name: "Signup",
        components:{
            vInput,
            vInputFile,
            vInputRadio
        },
        data(){
            return{
                inputs:[],
                inputChecked:false,
                positions:[],
            }
        },
        mounted(){
        //    this.getPosition('https://frontend-test-assignment-api.abz.agency/api/v1/positions');
    },
        methods:{
            inputUpdate(data){
                console.log(data)
                for (let i=0;i<this.inputs.length;i++){
                    if (!this.inputs[i].validation){
                        this.inputChecked=false;
                        break;
                    }
                    this.inputChecked=true;
                }
            },
            getPosition(url){
                fetch(url)
                    .then((response) => {
                        return response.json();
                    })
                    .then((data) => {
                     //   console.log(data)
                        this.positions=data.positions;
                    })
                    .catch(ex=>{
                       // console.log('parsing failed', ex)
                    });
            },
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

    .signup__radiobtn-container{
        display: flex;
        flex-direction: column;
        gap:12px;
    }

</style>