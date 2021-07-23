<template>
  <div class="background">
    <CustomerList />
  </div>

</template>

<script>
import CustomerList from './components/CustomersList.vue'

export default {
  name: 'App',
  components: {CustomerList},
}
</script>

<style>
  body {
    font-family: Rubik;
    font-size: 16px;
    font-style: normal;
    font-weight: 400;
    line-height: 25px;
    letter-spacing: 0px;
    text-align: left;
  }
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  .background {
    background: #F2F5FA;
  }

  @media only screen and (max-width: 400px) {
    body {
      font-family: Rubik;
      font-size: 13px;
      font-style: normal;
      font-weight: 400;
      line-height: 15px;
      letter-spacing: 0px;
      text-align: left;
    }
  }
  
</style>
