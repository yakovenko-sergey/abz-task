<template>
    <div class="hint__wrapper"
         v-show="hint.hintText"
         :style="hintPosition"
    >
        <p>{{hint.hintText}}</p>
    </div>
</template>

<script>
    export default {
        name: "Hint",
        props:{
            hint:{
                type:Object,
                require:true
            }
        },
        computed:{
            hintPosition: function () {
                return {'top':this.hint.positionY+25+'px'};
            }
        }
    }
</script>

<style scoped>
    .hint__wrapper{
        display: block;
        position: absolute;
        left:20px;
        white-space: break-spaces;
        max-width: 300px;
    }
    .hint__wrapper p{
        font-family: 'Nunito';
        font-style: normal;
        font-weight: 400;
        font-size: 16px;
        color:#fff;
        background: rgba(0, 0, 0, 0.87);
        border-radius: 4px;
        padding: 8px;
        z-index: 10;

        overflow-wrap: break-word;
    }
    .hint__wrapper p:hover{
        background: red;
        cursor: pointer;
    }
</style>