<template>
    <h2>table check list</h2>
    <label for="Year">
        <input type="checkbox" id="Year" value="Year" v-model="checkedViews.Year" @change="checkViews">
        Year
    </label>
    <label for="Month">
        <input type="checkbox" id="Monthly" value="Month" v-model="checkedViews.Month" @change="checkViews">
        Month
    </label>
    <label for="Weekly4">
        <input type="checkbox" id="Weekly4" value="Weekly4" v-model="checkedViews.Weekly4" @change="checkViews">
        Weekly 4
    </label>
    <label for="Weekly2">
        <input type="checkbox" id="Weekly2" value="Weekly2" v-model="checkedViews.Weekly2" @change="checkViews">
        Weekly 2
    </label>
    <label for="Weekly">
        <input type="checkbox" id="Weekly" value="Weekly" v-model="checkedViews.Weekly" @change="checkViews">
        Weekly
    </label>
    <label for="Daily">
        <input type="checkbox" id="Daily" value="Daily" v-model="checkedViews.Daily" @change="checkViews">
        Daily
    </label>
</template>

<script>
export default {
    emits:['checked-views'],
    data() {
        return{
            checkedViews: 
            {
                Year: true,
                Month: false,
                Weekly4: false,
                Weekly2: false,
                Weekly: true,
                Daily: true,
            }
        }
    },
    methods:{
        checkViews(){
            this.$emit('checked-views', this.checkedViews)
        }
    }
}
</script>

<style scoped>

</style>