<template>
  <div class="rowMap">
    <l-map :zoom="zoom" :center="geoloc(centre.lat, centre.lng)">
    <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
    <l-marker :key="index" v-for="(result, index) in results" :lat-lng="geoloc(result.location.geocode.lat, result.location.geocode.lng)">
       <l-icon :icon-size="iconSize" :icon-url="icon"/> 
        <l-popup :content="result.name" :options="{ autoClose: false, closeOnClick: false }"></l-popup>
    </l-marker>
  </l-map> 

  {{centre}}

  </div>
</template>

<script>
import L from 'leaflet'
import {LMap, LTileLayer, LMarker, LIcon, LPopup} from 'vue2-leaflet'
import food from '../assets/Food.png'
  export default { 
    name: "AutoraMap",
    props:{
      results:Array,
      centre: Object
    },
    data:function(){
      return{
      zoom:13,
      iconSize: [30,30],
      icon: food,
      url:'https://tile.thunderforest.com/transport/{z}/{x}/{y}.png?apikey=30bc173714a74f1391503ef7ad21adb0',
      attribution:'&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      marker: L.latLng(47.413220, -1.219482)}
    },
    components:{
      LMap,
      LTileLayer,
      LMarker,
      LIcon,
      LPopup
    },
    methods:{
      geoloc(lat, lng){ 
        return L.latLng(lat, lng);  
      },
    },
  }
</script>

<style scoped>
.rowMap {
  height: 100%;
}
.map {
  height: 95vh;
}
</style>
