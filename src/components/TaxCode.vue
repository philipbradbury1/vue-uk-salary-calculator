<template>
    <h2>Tax Code</h2>
    <p>If you know your tax code, please enter it here.</p>

    <p v-show="inputError">Please check your tax code!</p>
    <input @input="checkTaxCode" v-model="taxcode" @change="getTaxCode" type="text" name="taxcode">
</template>

<script>
export default {
    emits: ["tax-code"],
    data(){
        return{
            taxcode: "",
            inputError: false
        }
    },
    methods:{
        checkTaxCode(){

            const regEx = new RegExp("^(BR|D0|NT)$|^(([Kk]{1}[1-9]{1}[0-9]{2,3}$)|([1-9]{1}[0-9]{2,3}[LPTYlpty]{1}$))")

            if(!regEx.test(this.taxcode)){
              return  this.inputError = true;
            }
             
            return this.inputError = false;
        },
        getTaxCode(){
            if(!this.inputError){
                this.$emit("tax-code", this.taxcode)
            }
        }
    }
}

</script>

<style>

</style>