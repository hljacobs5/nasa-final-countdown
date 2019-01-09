<template>
  <div>
     <button v-on:click='getCurrentDayPicture()'>Today's Picture</button>
     <button v-on:click='getAllPics()'>Get All Pictures</button>
     <img class='current-picture' :src='this.currentDatePicture.picture' />
     <div class='pictures'>
      <img v-if='showAllPictures' v-for='result in results' :value='result.date' :src='result.picture' />
     </div>

  </div>
</template>

<script>
import axios from 'axios';
import { mockMonthData } from '../mockData/mockData';
const moment = require('moment')

export default {
  name: 'HelloWorld',
  data () {
    return {
      query: '',
      results: '',
      currentDatePicture: '',
      showAllPictures: '',
      currentDate: ''
    }
  },
    mounted() {
      this.getDate()
      this.getPics()
    },

  methods: {
    getDate() {
      const currentDate = Date.now()
      const dateString = moment(currentDate).format('YYYY-DD-MM')
      this.currentDate = dateString
    },

    getCurrentDayPicture() {
      this.showAllPictures = '';
      this.results.forEach(result => {
        if (result.date === this.currentDate) {
          this.currentDatePicture = result
        }
      })
    },

    getAllPics() {
      this.currentDatePicture = '';
      this.showAllPictures = this.results;
    },

    getPics() {

      // axios.get(mockMonthData)
      //   .then((response) => {
      //     console.log(response)
      //     // this.results = response.data.collection.items;
      //   })
      //   .catch((error) => {
      //     console.log(error)
      //   })
        console.log(mockMonthData, this.currentDate)
        this.results = mockMonthData
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .current-picture {

  }

  .pictures {
    display: flex;
    flex-wrap: wrap;
  }
</style>
