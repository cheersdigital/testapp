<template>
  <div class="p-5 sm:p-10">
    <p class="mb-5">Search for recently sold cards on eBay</p>
    <form class="flex w-full" @submit.prevent="searchCards">
      <input class="flex-1 w-auto rounded-l-lg p-4 border-t mr-0 pr-5 border-b border-l text-gray-800 border-gray-200 bg-white focus:outline-none" placeholder="i.e Tyler Herro 2019-20 Silver Mosaic Prizm" v-model="search" required />
      <button class="flex-shrink-0 px-8 rounded-r-lg bg-blue-700 text-white font-bold p-4 text-xs uppercase focus:outline-none">Lesh go!</button>
    </form>
    <!-- <p>{{cards.length}} APIs</p> -->
    <div class="flex items-center mt-5 sm:mt-10" v-for="card in cards">

      <img class="h-32 w-32 object-cover mr-5" :src="card.pictureURLSuperSize[0]">

      <!-- <a class="image" :href="card.viewItemURL[0]" :style="{ backgroundImage: 'url(' + card.galleryURL[0] + ')' }">

      </a> -->
      <!-- <img :src="card.galleryURL[0]"> -->
      <div>
        <a :href="card.viewItemURL[0]" target="_blank">{{ card.title[0] }}</a><br>
        <span>{{ formatDate(card.listingInfo[0].endTime[0]) }}</span>
        <div>
          <span>{{ formatPrice(card.sellingStatus[0].currentPrice[0].__value__) }}</span>
          <span v-if="card.sellingStatus[0].bidCount">({{ card.sellingStatus[0].bidCount[0] }} bids)</span>
          <span v-else>(BIN/BO)</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

  // let eBay = require('ebay-node-api')

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
        search: '',
        cards: []
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

      async searchCards() {
        console.log(this.search);

        // const ip = await this.$axios.$get('http://icanhazip.com')
        // this.ip = ip

        //('/api/v1?OPERATION-NAME=findCompletedItems&SERVICE-VERSION=1.0.0&SECURITY-APPNAME=TimBrown-WhatsMyC-PRD-f2eb6be68-8f9ce244&RESPONSE-DATA-FORMAT=JSON&REST-PAYLOAD&keywords=harry%20potter%20phoenix&paginationInput.entriesPerPage=2')

        const cards = await this.$axios.$get('/api/v1', {
          params: {
            'OPERATION-NAME': 'findCompletedItems',
            'SERVICE-VERSION': '1.4.0',
            'SECURITY-APPNAME': 'TimBrown-WhatsMyC-PRD-f2eb6be68-8f9ce244',
            'RESPONSE-DATA-FORMAT': 'JSON',
            'REST-PAYLOAD': null,
            'keywords': this.search,
            'paginationInput.entriesPerPage': '10',
            'EndTimeSoonest': null,
            'categoryId': '64482',
            'itemFilter.name': 'SoldItemsOnly',
            'itemFilter.value': true,
            'outputSelector': 'PictureURLSuperSize'
          }
        })

        this.cards = cards.findCompletedItemsResponse[0].searchResult[0].item



        // var items = cards.findCompletedItemsResponse[0].searchResult[0].item || []

        // for (var i = 0; i < cards.length; ++i) {
        //   var item = cards[i]
        //   var title = item.title
        //   var image = item.galleryURL

        //   this.cards.push(title, image);
        //   // this.cardsconsole.log(title, image);
        //   // html.push('<tr><td>' + '<img src="' + pic + '" border="0">' + '</td>' +
        //   //   '<td><a href="' + viewitem + '" target="_blank">' + title + '</a></td></tr>')

        // }




        console.log(this.cards);

        //var cards = JSON.stringify(results.findCompletedItemsResponse[0].searchResult[0].items)
        // this.cards = JSON.parse(JSON.stringify(cards))
        // this.cards = JSON.parse(cards);
        //cards.findCompletedItemsResponse[0].searchResult[0].item;

        //(JSON.parse(cards.findCompletedItemsResponse[0].searchResult[0].item))

        // for (var i = 0; i < cards.length; i++) {
        //   var d = card[i];
        //   console.log('title: ' + d.title);
        // };


        // console.log(this.cards);
        // alert(this.ip);

        // $axios
        //   .get('http://jsonplaceholder.typicode.com/posts')
        //   .then((response) => {
        //     return { cards: response.data }
        //   })
        //   .catch((response) => {
        //     console.log(response.data);
        //   });

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
      },

      formatPrice(value) {
        // return value.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1,');
        var formatter = new Intl.NumberFormat('en-US', {
          style: 'currency',
          currency: 'USD',
          minimumFractionDigits: 2
        })
        return formatter.format(value)
      },

      formatDate(value) {
        var date = new Date(value);
        var months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
        return months[date.getMonth()] + ' ' + date.getDate() + ', ' + date.getFullYear();
      }
    }

  }

</script>

<style>

</style>