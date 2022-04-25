<template>
    <div class="input__wrapper">
        <input
                @input="inputUpdate"
                @change="inputValidate"
                @click="phoneClick"
                :type="inputType"
                :placeholder="inputPlaceholder"
                v-model="inputProperty[inputProp].val"
                :class="inputProperty[inputProp].changeFlag && !inputProperty[inputProp].validation
                ?
                'input-error':'input-normal'"
        />
        <p>{{inputProperty[inputProp].changeFlag && !inputProperty[inputProp].validation
            ?
            inputProperty[inputProp].errorText:inputProperty[inputProp].helperText}}
        </p>
    </div>
</template>

<script>
    export default {
        name: "Inputs",
        props:{
            inputType:{
                type:String,
                require:true
            },
            inputProp:{
                type:String,
                require:true
            },
            inputPlaceholder:{
              type:String,
              require:true
            },
            inputsChild:{
                type:Array
            }
        },
        data(){
            return{
                inputProperty:{
                    name:{
                        alias:'name',
                        val:'',
                        helperText:'',
                        errorText:'The name may not be greater than 60 characters',
                        changeFlag:false,
                        validation:false,
                        pattern:'[A-z]{2,60}',
                    },
                    email:
                        {
                            alias:'email',
                            val:'',
                            helperText:'',
                            errorText:'at least 2-100 characters and format youremail@xxx.com',
                            changeFlag:false,
                            validation:false,
                            pattern:'^(?:[a-z0-9!#$%&\'*+/=?^_`{|}~-]+(?:\\.[a-z0-9!#$%&\'*+/=?^_`{|}~-]+)*|"' +
                                '(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21\x23-\x5b\x5d-\x7f]|\\\\' +
                                '[\x01-\x09\x0b\x0c\x0e-\x7f])*"){2,100}@(?:(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\\.)' +
                                '+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?|\\[(?:(?:25[0-5]| 2[0-4][0-9]|[01]?[0-9][0-9]?)\\.){3}' +
                                '(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?|[a-z0-9-]*[a-z0-9]:' +
                                '(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21-\x5a\x53-\x7f]|\\\\[\x01-\x09\x0b\x0c\x0e-\x7f])+)\\]$)'
                        },
                    phone:
                        {
                            alias:'phone',
                            val:'',
                            helperText:'+38 (XXX) XXX - XX - XX',
                            errorText:'The phone format is invalid (+38 (XXX) XXX - XX - XX)',
                            changeFlag:false,
                            validation:false,
                            pattern:'^[\\+]{1}38(\\(\\d+\\)+)\\s?(\\d){3}-(\\d){2}-(\\d){2}$'
                        }
                }
            }
        },
        mounted(){
            this.$props.inputsChild[this.inputProp]=this.inputProperty[this.inputProp];
        },
        methods:{
            phoneClick(e){
                if (e.target.type=='tel' && e.target.value=='') e.target.value='+38'
            },

            phoneMask(e){
                let input=e.target;
                let subInput='';
                let inputNumbersValue = input.value.replace(/\D/g, '');

                if (input.value.length != input.selectionStart) {
                    // Editing in the middle of input, not last symbol
                    if (e.data && /\D/g.test(e.data)) {
                        // Attempt to input non-numeric symbol
                        input.value = inputNumbersValue;
                    }
                    return;
                }


                subInput = input.value = "+38";
                console.log('Length->',inputNumbersValue)
                if (inputNumbersValue.length > 2) {
                    subInput += '(' + inputNumbersValue .substring(2, 5);
                }
                if (inputNumbersValue.length > 5) {
                    subInput += ') ' + inputNumbersValue .substring(5, 8);
                }
                if (inputNumbersValue.length > 8) {
                    subInput += '-' + inputNumbersValue .substring(8, 10);
                }
                if (inputNumbersValue.length > 10) {
                    subInput += '-' + inputNumbersValue .substring(10, 12);
                }

                console.log(subInput);
                this.inputProperty.phone.val=input.value=subInput;
            },

            inputUpdate(e){
                if (e.target.type=='tel'){
                    this.phoneMask(e);
                }
               this.$emit('inputUpdate',this.inputsChild);
            },

            inputValidate(){
                this.inputProperty[this.inputProp].changeFlag=true;
                let pattern=new RegExp(this.inputProperty[this.inputProp].pattern);
               (pattern.test(this.inputProperty[this.inputProp].val))?
                    this.inputProperty[this.inputProp].validation=true:this.inputProperty[this.inputProp].validation=false;
                this.$emit('inputUpdate',this.inputsChild);
            },
        }
    }
</script>

<style>
    .input__wrapper{
        user-select: none;
        width:100%;
    }
    .input__wrapper input{
        width:100%;
        height: 54px;
        box-sizing: border-box;
        border-radius: 4px;
        padding: 14px 16px;
    }

    .input-normal{
        border: 1px solid #D0CFCF;
    }

    .input-normal ~ p{
        color:#7E7E7E;
        font-size: 12px;
    }

    .input-error{
        border: 1px solid red;
    }

    .input-error ~ p{
        color:red;
        font-size: 12px;
    }

</style>