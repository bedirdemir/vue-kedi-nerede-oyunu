<template>
  <div id="app" class="container">
    <component
      :is="currentPage">

    </component>
  </div>
</template>

<script>
import appGameCards from './components/GameCards.vue'
import appSuccesPage from './components/SuccesPage.vue'
import appFailPage from './components/FailPage.vue'
import {EventBus} from './main'

export default {
  name: 'App',
  components: {
    appGameCards,
    appSuccesPage,
    appFailPage
  },
  data(){
    return {
      currentPage: "appGameCards",
      isReplay: null
    }
  },
  watch: {
    isReplay(value){
      if(value){
        this.currentPage = "appGameCards";
        this.isReplay = false;
      }
    }
  },
  created(){
    EventBus.$on("isSucces", (value) => {
      if(value == true){
        this.currentPage = "appSuccesPage";
      }else{
        this.currentPage = "appFailPage";
      }
    });

    EventBus.$on("isReplay", (value) => {
      this.isReplay = value;
    })
  }
}
</script>

<style>

</style>
