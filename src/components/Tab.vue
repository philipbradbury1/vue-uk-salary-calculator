<template>
  <div v-show='title == currentTab'>
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: 'Tab 1'
    },
    currentTab:{
        type: String,
        default: "Tab 1"
    }
  },
  data () {
    return {
        localSomeProp: null,

    }
  }
}
</script>