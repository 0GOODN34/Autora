<template>

  <div class="container">
    <div class="row">
      <div class="col-12">
        <h1 class="text-center text-info"> Autora Food List</h1>
        <p>Filter the Search</p>
        Group Type:
        <select  v-model="groupText" v-on:change="updateResults()">
          <option value="friends">Friends</option>
          <option value="solo">Solo</option>
          <option value="couple">Couple</option>
          <option value="kids">Kids</option>
          <option value="teenager">Teenager</option>
          <option value="group">Groups</option>
        </select> 

        Stop Type: 
           <select  v-model="stopType" v-on:change="updateResults()">
          <option value="poi">Point of Interest</option>
          <option value="food">Food</option>
          <option value="attraction">Attraction</option>
          <option value="tour">Tour</option>
          <option value="event">Event</option>
          <option value="accom">Accomodation</option>
        </select>
      </div>
    </div>
      <div class="row">
        <div class="col-6 ">
          <AutoraList @mouseClick="mouseClick" :results="results"/>
        </div>

        <div class="col-6">
              <AutoraMap :results="results" :centre="theCentre"/>
        </div>


      </div>
  </div>

</template>

<script>

  import { AUTORA_KEY } from '../config';
  import axios from 'axios'
  import AutoraList from './AutoraList.vue'
  import AutoraMap from './AutoraMap.vue'

export default {
  name: 'Autora',
  components: {AutoraList,AutoraMap},

  data: function () {
    return {
      key: AUTORA_KEY,
      results:[],
      groupText: "friends",
      stopType: "poi",
      show:false,
      theCentre: {
        lat: 51,
        lng: -1.01
      }
   }
 },
  mounted:function (){
    this.updateResults()

  },
  methods:{
    updateResults() {
 const inst = axios.create({ headers: { 'Authorization': 'Bearer ' + this.key } })
      inst.get('https://api.autoura.com/api/stops/search?group_context=' + this.groupText + '&stop_types=' + this.stopType).then(r => {
        this.results = r.data.response;
      }).catch(e => {
        (e);
     })
    },
    mouseClick:function(index){
      console.log(index +'mouseClick');
      console.log(this.results[index])
      this.theCentre = {
        lat: this.results[index].location.geocode.lat,
        lng: this.results[index].location.geocode.lng 
      }
    },
     getLocation() {
  if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition(this.showPosition);
      console.log()
    } else {
        console.log("geo lat not supported")
    }
      },
    showPosition(position) {
      console.log(position)
      this.theCentre = {
        lat: position.coords.latitude,
        lng: position.coords.longitude
      }
}
    },
    created() {
      this.getLocation()
    }
}
</script>


<style lang="scss" scoped>

</style>
