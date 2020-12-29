<template>
  <div id="app">
    <infotable :workers="workers" @changeworker="changeworker"></infotable>
  </div>
</template>

<script>
import Infotable from './components/Infotable.vue'

export default {
  name: 'App',
  components: {
    Infotable
  },
  data() {
    return {
      workers:[{
        firstname:'Stephen',
        lastname:'Walther',
        phone:'18976492374',
        email:'101046607@qq.com'
      },{
        firstname:'Benjamin',
        lastname:'Jones',
        phone:'13016481962',
        email:'1049549831@qq.com'
      },{
        firstname:'Helyn',
        lastname:'Orr',
        phone:'13385038402',
        email:'1203561046@qq.com'
      },{
        firstname:'Micheal',
        lastname:'Jordan',
        phone:'18857389293',
        email:'52240380@qq.com'
      }]
    }
  },
  methods:{
    changeworker(__finisheditworker,inde) {
      this.workers[inde]=__finisheditworker;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
