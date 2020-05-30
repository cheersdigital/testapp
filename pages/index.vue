<template>
  <div class="container">
    <!-- <div v-for="card in filteredCards">
      {{ card.title }}
    </div> -->

    <button class="p-4 rounded-lg bg-blue text-xs w-1/2 mt-6 ml-auto mr-auto" @click="searchCards">Search</button>
  </div>
</template>

<script>

  let eBay = require('ebay-node-api')

  // let ebay = new eBay({
  //   clientID: 'DmitryKh-8c0f-4272-80d0-a0df7dca76f8',
  //   env: 'SANDBOX', // optional default = 'PRODUCTION'
  //   headers: { // optional
  //     'X-EBAY-C-MARKETPLACE-ID': 'EBAY_US' // For Great Britain https://www.ebay.co.uk
  //   }
  // })

  export default {

    data: function () {
      return {
        //search: '',
        //results: [],
      }
    },

    // asyncData(context) {
    //   return context.$axios
    //     .get('http://jsonplaceholder.typicode.com/posts')
    //     .then((response) => {
    //       return { cards: response.data }
    //     })
    //     .catch((response) => {
    //       console.log(response.data);
    //     });
    // },

    methods: {

      searchCards() {
        // ebay.findItemsByKeywords({
        //   keywords: 'Garmin nuvi 1300 Automotive GPS Receiver',
        //   sortOrder: 'PricePlusShippingLowest', //https://developer.ebay.com/devzone/finding/callref/extra/fndcmpltditms.rqst.srtordr.html
        //   pageNumber: 2,
        //   limit: 10
        // }).then((data) => {
        //   console.log(data);
        // }, (error) => {
        //   console.log(error);
        // });
      }
    }

  }

</script>

<style>

</style>