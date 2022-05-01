<template>
    <div class="input-file__wrapper">
        <label :for="id" class="input-file__label" :class="inputProperty.file.changeFlag && !inputProperty.file.validation
        ?
        'input-error':'input-normal'">
            <p>Upload</p>{{inputProperty.file.placeholder}}
        </label>
        <input type="file" :id="id" accept=".jpg,.jpeg"
               @change="inputUpdate"
        />
        <p>{{inputProperty.file.changeFlag && !inputProperty.file.validation
            ?
            inputProperty.file.errorText:inputProperty.file.helperText}}
        </p>
    </div>
</template>

<script>
    export default {
        name: "InputsFile",
        props:{
            inputsChild:{
                type:Array
            },
            id:String
        },
        data(){
            return{
                inputProperty: {
                    file: {
                        alias: 'photo',
                        placeholder: 'Upload your photo',
                        val:'',
                        size:5000000,
                        aspectRatio:70,
                        helperText: '',
                        errorText: 'image must be 70x70 and no larger than 5MB',
                        changeFlag:false,
                        validation: false,
                    },
                }
            }
        },
        mounted(){
            this.$props.inputsChild[this.inputProperty.file.alias]=this.inputProperty.file;
        },
        methods: {
            inputUpdate(event) {
                let URL = window.URL || window.webkitURL;
                let fileData =  event.target.files[0];
                let img = new Image();
                img.src=URL.createObjectURL(fileData);
                img.onload = () => {
                    console.log(fileData)
                    if(img.width === this.inputProperty.file.aspectRatio && img.height === this.inputProperty.file.aspectRatio && fileData.size<=this.inputProperty.file.size){
                        this.inputProperty.file.validation=true;
                    }
                    else{
                        this.inputProperty.file.validation=false;
                    }
                    this.inputProperty.file.changeFlag=true;
                    this.inputProperty.file.placeholder=fileData.name;
                    this.inputProperty.file.val=fileData;
                    this.$emit('inputUpdate', this.inputsChild);
                }

            }
        }
    }
</script>

<style>
    .input-file__wrapper{
        display: flex;
        flex-direction: column;
    }
    .input-file__label{
        display: block;
        border: 1px solid #D0CFCF;
        box-sizing: border-box;
        border-radius: 4px;
        cursor: pointer;
        line-height: 54px;
        width: 100%;
        text-overflow: ellipsis;
        white-space: nowrap;
        overflow: hidden;
        background: white;
        margin: 33px 0 0;
    }
    .input-file__label p{
        display: inline-block;
        box-sizing: border-box;
        border-radius: 4px 0px 0px 4px;
        padding: 0 14px;
        margin: 0 16px 0 0;
    }

    .input-normal{
        border: 1px solid #D0CFCF;
    }
    .input-normal>p{
        border-right: 1px solid #D0CFCF;
        color:#7E7E7E;
    }


    .input-error{
        border: 1px solid red;
    }
    .input-error>p{
        border-right: 1px solid red;
        color:red;
    }

    input[type="file"] {
        display: none;
    }

</style>