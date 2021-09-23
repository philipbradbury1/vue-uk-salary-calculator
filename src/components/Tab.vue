<template>
  <div v-show='title == currentTab' class="panel">
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: 'Tab'
    },
    currentTab:{
        type: String,
        default: "Tax Code"
    }
  },
  data () {
    return {
        localSomeProp: null,

    }
  }
}
</script>

<style>
    .panel{
        
        flex: 100%;
    }
</style>