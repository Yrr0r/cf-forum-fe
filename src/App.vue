<template>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css">
    <section class="section">
        <keep-alive><Homepage v-if="currentView == 'Homepage' " v-on:viewThread="changeToThreadView" /></keep-alive>

        <button v-if="currentView == 'ViewThread' " v-on:click="currentView = 'Homepage'"> Back to Homepage </button>
        <ViewThread v-if="currentView == 'ViewThread' " v-bind:nodeid="nodeId" />

        
    </section>

</template>



<script>
import Homepage from './components/Homepage.vue'
import ViewThread from './components/ViewThread.vue'

export default {
  name: 'App',
  components: {
    Homepage, ViewThread
  },
  data(){return{
    currentView: "Homepage",
    nodeId: '',

  }},
  methods:{
    changeToThreadView(thread){
      this.nodeId = thread;
      this.currentView = 'ViewThread';
    }
  }
}
</script>
