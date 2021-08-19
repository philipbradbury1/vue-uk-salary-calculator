<template>
    <h2>Student Loan</h2>
      <label for="repaymentplan1">
        <input type="checkbox" id="repaymentplan1" value="repaymentplan1" v-model="checkedLoans.repaymentplan1" @change="checkLoans">
        Repayment Plan 1
    </label>
    <label for="repaymentplan2">
        <input type="checkbox" id="repaymentplan2" value="repaymentplan2" v-model="checkedLoans.repaymentplan2" @change="checkLoans">
        Repayment Plan 2
    </label>
    <label for="postgradloan">
        <input type="checkbox" id="postgradloan" value="postgradloan" v-model="checkedLoans.postgradloan" @change="checkLoans">
        Postgraduate Loan
    </label>
</template>

<script>
export default {
    emits:['checked-loans'],
    data(){
        return{
            checkedLoans:{
                repaymentplan1: false,
                repaymentplan2: false,
                postgradloan: false
            }
        }
    },
    methods:{
        checkLoans(){
            this.$emit('checked-loans', this.checkedLoans)
        }
    }
}
</script>

<style>

</style>