<template>
  <div>

     <button v-on:click='getPics()'>Click me</button>
     <div class='results'>{{results}}</div>        
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
      currentDate: ''
    }
  },
    mounted() {
      this.getDate()
    },

  methods: {
    getDate() {
      const currentDate = Date.now()
      const dateString = moment(currentDate).format('YYYY-DD-MM')
      this.currentDate = dateString
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
        this.results = mockMonthData.map(day => {
          day.picture
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
