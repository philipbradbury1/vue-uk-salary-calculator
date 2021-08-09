<template>
    <h2>table check list</h2>
    <input type="checkbox" id="year" value="year" v-model="checkedViews" @change="checkViews">
    <input type="checkbox" id="monthly" value="month" v-model="checkedViews" @change="checkViews">
    <input type="checkbox" id="weekly4" value="weekly4" v-model="checkedViews" @change="checkViews">
    <input type="checkbox" id="weekly2" value="weekly2" v-model="checkedViews" @change="checkViews">
    <input type="checkbox" id="weekly" value="weekly" v-model="checkedViews" @change="checkViews">
    <input type="checkbox" id="daily" value="daily" v-model="checkedViews" @change="checkViews">

    

</template>

<script>
export default {
    emits:['checked-views'],
    data() {
        return{
            checkedViews: []
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