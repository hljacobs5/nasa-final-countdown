<template>
  <main>
    <section class='btn-container'>
      <button v-on:click='getCurrentDayPicture()'>Today's Photo</button>
      <button v-on:click='getAllPics()'>Collection of Current Month's Photos</button>
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
    background-color: #FFFFFF;
    color: #71298F;
    height: 40px;
    font-size: 20px;
    margin-bottom: 30px;
    cursor: pointer;
    border-radius: 12px;
    font-family: 'Coiny';
  }

  .current-picture {
    border: none;
    height: 30rem;
    width: 35rem;
    border-radius: 8px;
    border: 1.5px solid #FFFFFF;
  }

  .pictures {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
  }

  .picture {
    height: 20rem;
    width: 25rem;
    border-radius: 8px;
    border: 1.5px solid #FFFFFF;
  }

  .labels {
    display: flex;
    flex-direction: column;
    color: #FFFFFF;
    font-family: 'Coiny', cursive;
  }
</style>
