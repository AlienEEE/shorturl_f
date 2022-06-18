<template>
  <div class="shorturl">
    <div class="head">
      <b-navbar type="dark" variant="dark">
      <b-navbar-nav>
        <h2>SHORT URL</h2>
      </b-navbar-nav>
      </b-navbar>
    </div>
    <div class="input">
      <b-form-input v-model="add.long_url" placeholder="Enter link url"></b-form-input>
      <div class="button">
        <br>
         <b-button v-b-toggle.collapse-2 class="m-1" @click="posturl">short link</b-button>
      </div>
    </div>
    <div class="table" >
    <b-table striped hover :items="url" :fields="fields" bordered="true" outlined="true" >      
      <template #cell(short_url)="row" >
        http://localhost:3000/{{row.value}}
      </template> Stort</b-table>
  </div>
  </div>
</template>
<script>
import axios from 'axios'
  export default {
    data() {
      return {
        url:[],
        add:{long_url:""},
        apiURL: 'http://localhost:3000/api/get-all-short-urls',
        apiURL2: 'http://localhost:3000/api/short-url',
        fields:[
          {
            key:'long_url',
            label: 'long url',
            sortable: true
          },
          {
            key:'short_url',
            label: 'short url'
          },
          {
            key:'count',
            label: 'count',
            
          }
        ],
        
      }
    },
     computed: {
    row() {
      return this.boats.length
    },
  },
    async mounted() {
    const result1 = await axios.get(this.apiURL)
    this.url = result1.data
    console.log(result1);
  },
  methods:{
    async posturl(){
      const result = await axios.post(this.apiURL2,this.add)
      console.log(result);
      // this.$router.go()
    }
  }
  }
</script>

<style scoped>

  .head{
    height: 30px;
    margin-bottom: 100px;
  } 
  .input{
  width: 50%;
  margin-left: 25%;
  margin-top: 30px;
  text-align: center;
 }
 .table {
  /* display: flex; */
  width: 80%;
  text-align: center;
  margin-left: 10%;
  margin-top: 60px;
  
 }



 h2{
  color: rgb(174, 168, 168);
 }
</style>