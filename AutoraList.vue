<template>
<div class="card Autora-list">
  <ul class="list-group list-group-flush">
      <li @mouseclick="mouseClick(index)" v-bind:key="index" v-for="(result, index) in results" class="list-group-item">{{result.name}}{{result.group_context}} </li>
 </ul>
</div>
</template>

<script>

import { AUTORA_KEY } from '../config';
import axios from 'axios'
  export default {
    name: "AutoraList",
    data: function () {
      return {
        key: AUTORA_KEY,
        results:[],
        show:false
     }
   },
   methods:{
     mouseClick:function(index){
       this.$emit('mouseClick',index)
     }
   },
    mounted:function (){
      const inst = axios.create({ headers: { 'Authorization': 'Bearer ' + this.key } })
      inst.get('https://api.autoura.com/api/stops/search?group_context=friends&stop_types=food').then(r => {
        this.results = r.data.response;
      }).catch(e => {
        (e);
      })
    }
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
