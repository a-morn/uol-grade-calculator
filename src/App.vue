<template>
  <Header />
  <Calculator />
  <Footer />
</template>

<script>
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
import Calculator from './components/Calculator.vue'

export default {
  name: 'App',
  components: {
    Header,
    Calculator,
    Footer
  }
}
</script>

<style>

body {
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #E9A24A;
  background: #517E77;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  min-height: 100vh;
}

Header, Footer {
  width: 100%;
  display: flex;
  justify-content: center;
}

</style>
