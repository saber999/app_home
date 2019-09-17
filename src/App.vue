<template>
  <div id="app">
    test
  </div>
</template>
<script>
import Head from './components/head.vue';
import Banner from './components/banner.vue';
import Entries from './components/entries.vue';
import Welfare from './components/welfare.vue';
import Nav from './components/nav.vue';
import Adviser from './components/adviser.vue';
import Aboutus from './components/aboutus.vue';
import Company from './components/company.vue';
import Contact from './components/contact.vue';
import {replaceChn} from './js/util.js'
export default {
  name: 'app',
  components: {
    Head,
    Banner,
    Entries,
    Welfare,
    Nav,
    ProductList,
    Adviser,
    Aboutus,
    Company,
    Contact
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
