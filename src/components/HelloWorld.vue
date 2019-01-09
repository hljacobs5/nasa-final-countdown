<template>
  <main>
    <section class='btn-container'>
      <button v-on:click='getCurrentDayPicture()'>Today's Picture</button>
      <button v-on:click='getAllPics()'>Get All Pictures</button>
    </section>
    <section class='image-container'>

       <img class='current-picture' v-if='currentDatePicture' :src='this.currentDatePicture.picture' />
       <div class='pictures'>
        <img class='picture' v-bind:class='{}' v-if='showAllPictures' v-for='result in results' :value='result.date' :src='result.picture' />
       </div>
    </section>
  </main>
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
  main {
    display: flex;
    flex-direction: column;
  }

  button {
    background-color: black;
    color: white;
    height: 40px;
    font-size: 15px;
    margin-bottom: 30px;
  }

  .current-picture {
    border: none;
    height: 20rem;
    width: 25rem;
  }

  .pictures {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
  }

  .picture {
    padding-bottom: 30px;
    height: 20rem;
    width: 25rem;
  }
</style>
