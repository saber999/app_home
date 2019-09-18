<template>
  <div id="app">
    <Head></Head>
    <Banner :bannerData ="originData.indexBanner" ></Banner>
    <Entries :hasPaidConsult="originData.hasPaidConsult"></Entries>
    <Welfare :isNew="originData.isNew"></Welfare>
    <Nav></Nav>
    <Adviser></Adviser>
    <Aboutus></Aboutus>
    <Company></Company>
    <Contact></Contact>
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
import fetch from './js/axios.js'
export default {
  name: 'app',
  data(){
    return{
      originData: null,
      originProductData: null,
      proDatamap: null,
    }
  },
  components: {
    Head,
    Banner,
    Entries,
    Welfare,
    Nav,
    Adviser,
    Aboutus,
    Company,
    Contact
  },
  created(){
    Promise.all([fetch('/index/getIndexData'), fetch('/index/getAppIndexData')]).then(res=>{
      console.log(res)
      const [res1, res2] = res
            if(res1.ret == 0) {
                this.originData = res1.data
            }
            if(res2.ret == 0){
                
                this.originProductData = res2.data
                 if (this.originProductData && this.originProductData.productList && this.originProductData.productList.length > 0) {
                        this.originProductData.productList.forEach((item) => {
                        let urlLink = decodeURIComponent(item.src);
                        urlLink = replaceChn(urlLink, 'ssr');
                        item.url = encodeURIComponent(urlLink);
                        if (item.favorpack) {
                            console.log(item.favorpack)
                            for(let j = 0, len = item.favorpack.length; j < len; j ++) {
                            if (item.favorpack[j].class == '1' && item.favorpack[j].platformType && item.favorpack[j].platformType.indexOf('4') !== -1) {
                                item.isShowFavorpack = true;
                                break;
                            }
                            item.isShowFavorpack = false;
                            }
                        }
                        let id = item.productId || '';
                        let classId = (item.insuranceClassify && item.insuranceClassify.id != null) ? item.insuranceClassify.id : '';
                        let src = item.src || '';
                        let key = `${id}+${classId}+${src}`;
                        // this.proDatamap[key] = item;
                    });
                }
            }
    })
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
