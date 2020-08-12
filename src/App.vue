<template>
  <div id="app">
    <Home/>
  </div>
</template>

<script>
import Home from './components/home-component/home'

export default {
  name: 'App',
  components: {
    Home
  }
}
</script>

<style>
body{
  background-image: url(https://paulryan.com.au/wp-content/uploads/2015/01/high-resolution-wallpapers-25.jpg);
  background-position: center center;
  background-size: cover;
  background-repeat: no-repeat;
  background-attachment: fixed;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
