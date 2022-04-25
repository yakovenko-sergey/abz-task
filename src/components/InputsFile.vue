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
                        Size:70,
                        aspectRatio:70,
                        helperText: '',
                        errorText: 'Size 70x70',
                        changeFlag:false,
                        validation: false,
                    },
                }
            }
        },
        mounted(){
            this.$props.inputsChild[this.inputProperty.file.alias]=this.inputProperty.file;
           // this.$props.inputsChild.push(this.inputProperty.file)
        },
        methods: {
            inputUpdate(event) {
                let URL = window.URL || window.webkitURL;
                let fileData =  event.target.files[0];
                let img = new Image();
                img.src=URL.createObjectURL(fileData);
                img.onload = () => {
                    if(img.width === this.inputProperty.file.aspectRatio && img.height === this.inputProperty.file.aspectRatio){
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
        border: 1px solid rgba(0, 0, 0, 0.87);
        box-sizing: border-box;
        border-radius: 4px 0px 0px 4px;
        padding: 0 14px;
        margin: 0 16px 0 0;
    }

    .input-normal,.input-normal>p{
        border: 1px solid #D0CFCF;
    }

    .input-normal ~ p{
        color:#7E7E7E;
        font-size: 12px;
    }

    .input-error, .input-error>p{
        border: 1px solid red;
    }

    .input-error ~ p{
        color:red;
        font-size: 12px;
    }

    input[type="file"] {
        display: none;
    }

</style>