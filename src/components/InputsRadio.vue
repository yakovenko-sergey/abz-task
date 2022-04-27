<template>
    <div class="input-radio__wrapper" ref="inputsRadio">
        <div class="input-radio__item"
             v-for="item in items"
             :key="item">
            <input
                    @change="inputValidate"
                    type="radio"
                    :name="groupName"
                    :value="item.name"
                    :positionId="item.id"
                    :id="item.name+'-'+groupName"
            />
            <label :for="item.name+'-'+groupName">{{item.name}}</label>
        </div>
        <p style="color:red">
            {{inputProperty.radio.changeFlag && !inputProperty.radio.validation?
            inputProperty.radio.errorText:inputProperty.radio.helperText}}
        </p>
    </div>
</template>

<script>
    export default {
        name: "InputsRadio",
        props:{
            inputsChild:{
                type:Array
            },
            items:{
                type:Array
            },
            groupName:String
        },
        data(){
            return {
                inputProperty: {
                    radio: {
                        alias:'position_id',
                        val:'',
                        helperText: '',
                        errorText: 'Select your position please',
                        positionId:'',
                        changeFlag: false,
                        validation: false,
                    },
                }
            }
        },
        mounted(){
            this.$props.inputsChild[this.inputProperty.radio.alias]=this.inputProperty.radio;
        },
        methods:{
            inputValidate(e){
                this.inputProperty.radio.val=e.target.getAttribute('positionId');
                this.inputProperty.radio.changeFlag=true;
                this.$nextTick(()=>{
                    let inputs = this.$refs.inputsRadio.querySelectorAll('input');
                     for (let i=0;i<inputs.length;i++){
                        if (inputs[i].checked){
                            this.inputProperty.radio.validation=true;
                            break;
                        }
                        this.inputProperty.radio.validation=false;
                    }
                    this.$emit('inputUpdate',this.inputsChild);
                })
            }
        }
    }
</script>

<style>
    .input-radio__wrapper{
        display: flex;
        flex-direction: column;
        gap:12px;
    }
</style>