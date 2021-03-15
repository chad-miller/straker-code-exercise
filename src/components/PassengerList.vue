<template>
  <div class="overflow-auto">

    <h1>Passenger List</h1>
 
     <b-pagination
      v-model="currentPage"
      :total-rows="rows"
      :per-page="perPage"
      aria-controls="my-table"
      align="center"
      size="lg"
    ></b-pagination>
  

    <p class="mt-3">Current Page: {{ currentPage }}</p>

    <b-row>
      <b-col md="3">
        <b-form-input v-model="filter" type="search" placeholder="Search passengers"></b-form-input>
      </b-col>
    </b-row>

    <b-row>
      <b-col>
        <b-table id="my-table" :items="list" :per-page="perPage" :current-page="currentPage" :filter="filter"  striped hover></b-table>
      </b-col>
    </b-row>

    <b-pagination
      v-model="currentPage"
      :total-rows="rows"
      :per-page="perPage"
      aria-controls="my-table"
      align="center"
      size="lg"
    ></b-pagination>

  </div>
    
</template>
<script>
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios";
Vue.use(VueAxios, axios)
export default {
  name: "PassengerList",
  data() {
    return {
      perPage: 20,
      currentPage: 1,
      list: [],
      filter: ''
    }     
  },
   computed: {
      rows() {
        return this.list.length
      }
    },
    
  mounted() {
    Vue.axios.get('http://coding-task.strakertranslations.com/passengers')
    .then(res => this.list = res.data)
    .catch(err => console.log(err))
  }
}
</script>

<style scoped>
  h1{
    margin-bottom: 1.5rem;
  }
  input {
    margin-bottom: 1.5rem;
  }
  b-pagination {
    display: flex;
    justify-content: center;
  }
  input{
    margin-left: 2rem;
  }
</style>

