<template>
    <div><h2>Enter your salary here for a full breakdown £
    <input v-model="salary" type="number" name="salary"></h2></div>
    <button @click="getNewSalary">Submit</button>

</template>

<script>
export default {
    data(){
       return {
           salary: '',
       }

   },
   emits:['new-salary'],
   methods: {
       getNewSalary(){
           this.$emit('new-salary', this.salary)
       }
   }
}
</script>

<style scoped>

</style>