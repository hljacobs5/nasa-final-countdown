<template>
  <main>
    <section class='btn-container'>
      <button v-on:click='getCurrentDayPicture()'>Today's Picture</button>
      <button v-on:click='getAllPics()'>Get this month's pictures</button>
    </section>
    <section class='image-container'>
       <img class='current-picture' v-if='currentDatePicture' :src='this.currentDatePicture.url' />
       <div class='pictures'>
       <template class='labels' v-for='result in results' v-if='showAllPictures'>
         <div class='labels'>
            <img class='picture' v-bind:class='{}' v-if='showAllPictures' :value='result.date' :src='result.url' />
            <p>{{result.date}}</p>
          </div>
        </template>
       </div>
    </section>
  </main>
</template>

<script>
import axios from 'axios';
import { mockMonthData } from '../mockData/mockData';
const moment = require('moment');
import { apiKey } from '../key.js';

export default {
  name: 'HelloWorld',
  data () {
    return {
      query: '',
      results: '',
      currentDatePicture: '',
      showAllPictures: '',
      currentDate: '',
      currentMonth: ''
    }
  },
  
  created() {
    this.getDate()
    this.getPics()
  },

  methods: {
    getDate() {
      const currentDate = Date.now()
      const dateString = moment(currentDate).format('YYYY-MM-DD')
      this.currentDate = dateString
      const currentMonth = moment(currentDate).format('YYYY-MM')
      this.currentMonth = currentMonth + '-01'
      console.log(dateString)
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
      // axios.get(`https://api.nasa.gov/planetary/apod?api_key=${apiKey}&start_date=${this.currentMonth}`)
      //   .then((response) => {
      //     console.log('kkklll', response.data)
      //     this.results = response.data;
      //     this.currentDayPicture = response.data.slice(-1)[0];
      //   })
      //   .catch((error) => {
      //     console.log(error)
      //   })

      this.results = mockMonthData.data;
      this.currentDayPicture = mockMonthData.data.slice(-1)[0];
    }
  }
}
</script>

<style scoped>
  main {
    display: flex;
    flex-direction: column;
  }

  button {
    background-color: grey;
    color: white;
    height: 40px;
    font-size: 15px;
    margin-bottom: 30px;
    border: none;
    cursor: pointer;
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

  .labels {
    display: flex;
     flex-direction: column;
  }
</style>
