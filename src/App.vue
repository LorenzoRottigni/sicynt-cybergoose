<template>
  <div id="app" class="d-flex flex-column m-0 p-0">
    <header>
      <h1 class="text-white text-center py-3 my-0 shadow-3">CYBERGOOSE GAME</h1>
    </header>
    
    <Main/>

    
    
  </div>
</template>

<script>
import Main from './components/Main.vue'

export default {
  name: 'App',
  components: {
    Main
  },
  data(){
      return {
        advisorHandler : false
      }
    }
  
}
</script>

<style lang="sass">
  @import url('https://fonts.googleapis.com/css2?family=Monofett&display=swap')
  header h1
    font-family: 'Monofett', cursive
    font-size: 60px
    background-color: rgba(181, 12, 0, 0.6)
    border-bottom: solid 1px white
  *
    box-sizing: border-box
  #app
    background-image: url('./assets/Cybereroe-SICYNT.png')
    background-size: cover
    background-repeat: no-repeat
    height: 100vh

</style>
