<template>
     <tr v-if="item.show" class="coloum-width">
        <td class="cell">{{item.name }}</td>
        <td v-for="(data, index) in salaryValue" :key="`tr-${index}`" class="cell salary-value">
            £ {{data}}
        </td> 
      </tr>
</template>

<script>
export default {
    props:['item', 'salary'],
    data(){
        return{

        }
    },
    computed:{
        salaryValue: function(){
            return this.salaryConvert(this.salary).filter(function(s){
                return s > 0 
            })
        }
    },
    methods:{
        salaryConvert(salary){

            if(this.item.name == 'Year'){
                console.log(salary)
                return salary.map(x => x.toFixed(2) );
            }
            if(this.item.name == 'Month'){
                 const month = this.salary.map(x => (x / 12).toFixed(2))
                return month
            }
            if(this.item.name == 'Weekly4'){
                const week = this.salary.map(x => (x / 13).toFixed(2))
                return week
            }
            if(this.item.name == 'Weekly2'){
                const week = this.salary.map(x => (x / 26).toFixed(2))
                return week
            }

            if(this.item.name == 'Weekly'){
                const week = this.salary.map(x => (x / 52).toFixed(2))
                return week
            }
            if(this.item.name == 'Daily'){
                const week = this.salary.map(x => (x / 260).toFixed(2))
                return week
            }
        }
    }
}
</script>

<style>

</style>