<template>
    <div class="panel">
        <div><h2>Enter your salary here for a full breakdown £
        <input v-model="salary" type="number" name="salary"></h2></div>
        <button @click="getNewSalary">Calculate</button>
    </div>

</template>

<script>
export default {
    emits:['new-salary'],
    data(){
       return {
           salary: '',
       }

   },
   methods: {
       getNewSalary(){
           this.$emit('new-salary', this.salary)
       }
   }
}
</script>

<style scoped>

.panel{
    background: #fff;
    border-radius: 10px;
    -webkit-box-shadow: 4px 4px 15px 0px #000000; 
box-shadow: 4px 4px 15px 0px #000000;
margin-bottom: 80px;
padding: 20px;
}

</style>