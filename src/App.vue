<template>
  <div id="app">
  	<TheHeader/>
    <!--<router-view/>-->
  </div>
</template>

<script>
	import TheHeader from '@/components/TheHeader'
export default {
  name: 'App',
  components:{
  	TheHeader
  }
}
</script>

<style>
*{margin: 0;padding: 0;}
ul,li{list-style: none;}
input,button{outline: none;border: none;}
#app {
  font-family: "microsoft yahei", Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 60px;
}

</style>
