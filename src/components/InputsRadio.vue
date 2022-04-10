<template>
    <div class="signup__radiobtn-container">
        <div class="signup__position-item"
             v-for="(item,index) in positions"
             :key="item">
            <input
                    :checked="index===0 ? true:false"
                    @input="updateValue"
                    type="radio" name="position"
                    :value="item.name"
                    :id="item.name">
            <label :for="item.name">{{item.name}}</label>
        </div>
    </div>
</template>

<script>
    export default {
        name: "InputsRadio"
    }
</script>

<style>

</style>