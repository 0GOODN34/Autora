<template>
  <div class="rowMap">

    <l-map :zoom="zoom" :center="center">
    <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
    <l-marker :key="index" v-for="(result, index) in results" :latlng="latLng(result.lat,result.lng)">
    <l-icon :icon-size="iconSize":icon-url="icon"
    </l-marker>
  </l-map>



  </div>
</template>

<script>
import {LMap, LTileLayer, LMarker, LIcon} from 'vue2-leaflet'
import food from '../assets/Food.png'
  export default {
    name: "AutoraMap",
    props:{
      results:Array
    },
    data:function(){
      return{
      zoom:13,
      center: L.latLng(47.413220, -1.219482),
      url:'https://tile.thunderforest.com/transport/{z}/{x}/{y}.png?apikey=30bc173714a74f1391503ef7ad21adb0',
      attribution:'&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      marker: L.latLng(47.413220, -1.219482)}
    },
    components:{
      LMap,
      LTileLayer,
      LMarker,
      LIcon
    },
    methods:{
      latLng: function(lat, lng){
        return L.latLng(lat, lng);
      },

    }
  }
</script>

<style scoped>
  .map{
    height:95vh;
  }
</style>
