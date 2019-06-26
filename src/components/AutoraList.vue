<template>
<div class="card Autora-list">
  <ul class="list-group list-group-flush">
      <li v-on:click="mouseClick(index)" v-bind:key="index" v-for="(result, index) in results" class="list-group-item">{{result.name}}{{result.group_context}} </li>
 </ul>
</div>
</template>

<script>

import { AUTORA_KEY } from '../config';
import axios from 'axios'
  export default {
    name: "AutoraList",
     props:{
      results:Array,
      
    },
    data: function () {
      return {
        key: AUTORA_KEY,
        results:[],
        show:false
     }
   },
   methods:{
     mouseClick(index){
       this.$emit('mouseClick',index)
     }
   },
   
  }
</script>

<style lang="scss" scoped>
.Autora-list{
  overflow-y: scroll;
  height: 95vh;
  li {
      &:hover {
      background-color:darkgrey;
            }

    }
}

</style>
