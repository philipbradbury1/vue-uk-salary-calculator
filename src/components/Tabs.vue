<template>
   <div class="tabs-container">
    <ul class='tabs__header'>
      <li v-for='tab in tabTitles' 
      :key='tab'
      :class="{ selected: tab == currentTab}"
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
      currentTab: "Tax Code"
    }
  },
  created () {
    
    this.tabTitles = this.$slots.default().map((tab) => tab.props.title);
   // this.title = this.tabTitles[0];

  },
  methods:{
    selectedTitle(tab){
        this.currentTab = tab
        this.$emit( 'tab-name' , tab)
    }
  }
  
}
</script>

<style scoped>

.tabs-container{
  display: flex;
  flex: 100%;
  border: 1px solid #cfcfcf;
 border-radius: 10px;
 background: #fff;
-webkit-box-shadow: 4px 4px 15px 0px #000000; 
box-shadow: 4px 4px 15px 0px #000000;
}



.tabs{
    max-width: 400px;
    margin: 0 auto;
}

.tabs__header {
    margin: 0px;
    list-style: none;
    padding: 0;
    width: 200px;
    display: flex;
    flex-direction: column;
    background: #6be790;
}

.tabs__header li{
    width: auto;
    text-align: center;
    padding: 10px 20px;
    background: #6be790;
    cursor: pointer;
    transition: 0.4s all ease-out;
    color: #fff;
}

.tabs__header li.selected{
    background-color: #0cb157;
    color: #fff;
}



</style>