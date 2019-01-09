<template>
  <div>
     <button v-on:click='getCurrentDayPicture()'>Today's Picture</button>
     <img :src='this.currentDatePicture.picture' />

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
      console.log('hit')
      this.results.forEach(result => {
        if (result.date === this.currentDate) {
          this.currentDatePicture = result
        }
      })
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

</style>
