<template>
    <h2>Pension</h2>
    <!--Do you contribute to a pension? -->
    <label>
        I contribute
        <input type="number" v-model="pension" @input="getPensionAmount">%
    </label>
</template>

<script>
export default {
    emits:['pension-amount'],
    data(){
        return{
            pension: null
        }
    },
    methods:{
        getPensionAmount(){
            this.$emit('pension-amount', this.pension)
        }
    }
}
</script>

<style>

</style>