<template>

  <div class="container">
    <div class="row">
      <div class="col-12">
        <h1 class="text-center text-info"> Autora Food List</h1>
      </div>
    </div>
      <div class="row">
        <div class="col-6 ">
          <AutoraList @mouseClick="mouseClick"/>
        </div>

        <div class="col-6">
              <AutoraMap :results="results"/>
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
      show:false
   }
 },
  mounted:function (){
    const inst = axios.create({ headers: { 'Authorization': 'Bearer ' + this.key } })
      inst.get('https://api.autoura.com/api/stops/search?group_context=friends&stop_types=food').then(r => {
        this.results = r.data.response;
      }).catch(e => {
        (e);
     })

  },
  methods:{
    mouseClick:function(index){
      console.log(index +'mouseClick');
    },
  }

}
</script>


<style lang="scss" scoped>

</style>
