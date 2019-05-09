<template>
  <div id="app">
    <h3>Latest Rates</h3>

    <div class="currency">
      <h3>EUR</h3>
      <span>{{ eur }}</span>
    </div>

    <div class="currency">
      <h3>USD</h3>
      <span>{{ usd }}</span>
    </div>

    <div class="currency">
      <h3>CAD</h3>
      <span>{{ cad }}</span>
    </div>

    <div class="currency">
      <h3>GBP</h3>
      <span>{{ gbp }}</span>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "app",
  data(){
    return{
      eur:0,
      usd:0,
      cad:0,
      gbp:0
    }
  },
  created() {

    // first step: get logged
    // second step: store the token into the local storage
    // third step: const apikey = localstorage.get('token') where localstorage is a javascript object

    const apiKey = "91a29c16d72da27786e077dbf32a1732";
    const url = 'http://data.fixer.io/api/latest?access_key=' + apiKey + '&base=EUR&symbols=USD,EUR,CAD,GBP';

    axios.get(url).then((res) => {
      //console.log(res);
      if (res.status === 200 && res.data.success) { // pour verifier que ma requete correctement executée
        this.usd = res.data.rates.USD;  // pour recuperer les données dans les objets de la réponse
        this.eur = res.data.rates.EUR;
        this.cad = res.data.rates.CAD;
        this.gbp = res.data.rates.GBP;
      }
    });
  }
};
</script>

<style lang="scss">
#app {
  font-family: Verdana, Geneva, Tahoma, sans-serif;

  .currency {
    display: inline-block;
    background: rgba(0, 0, 0, 0.1);
    padding: 10px 30px;
    margin: 10px;
    text-align: center;
    border: 1px solid lightgray;
  }
}
</style>
