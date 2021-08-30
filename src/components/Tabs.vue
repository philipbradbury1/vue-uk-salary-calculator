<template>
   <div>
    <ul class='tabs__header'>
      <li v-for='tab in tabTitles' 
      :key='tab'
      @click="selectedTitle(tab)"
      >
        {{ tab }} 
      </li>
    </ul>
    <slot></slot>
  </div>
</template>

<script>
export default {
    emits:['tab-name'],
  data () {
    return {
      selectedIndex: 0, 
      tabTitles: [],      
      title: "Tab 1"
    }
  },
  created () {
    
    this.tabTitles = this.$slots.default().map((tab) => tab.props.title);
    this.title = this.tabTitles[0];

  },
  methods:{
    selectedTitle(tab){
        this.$emit( 'tab-name' , tab)
    }
  }

  
  
}
</script>

<style>

</style>