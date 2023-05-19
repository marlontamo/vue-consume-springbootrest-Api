<template>
    <div>
        <H3>{{ msg }}</H3>
        <hr/>
        <input type="text" id="searchbar" v-model="search"/>
        <button v-on:click="find">search</button>
       <table class="table">
        <thead>
        <tr>
            <td scope="col">project Id</td>
            <td scope="col">projectName</td>
            <td scope="col">date Of Start</td>
            <td scope="col">teamSize</td> 
            <td scope="col">action</td>  


        </tr>
    </thead>
    <tbody>
        <tr v-for="data in info" :key="data.projectId">
            <td scope="row">{{ data.projectId }}</td>
            <td scope="row">{{ data.projectName }}</td>
            <td scope="row">{{ data.dateOfStart }}</td>
            <td scope="row">{{ data.teamSize }}</td>
            <td scope="row">
                <div class="btn-group" role="group" aria-label="Basic mixed styles example">
  <button type="button" class="btn btn-success">View</button>
  <button type="button" class="btn btn-warning">Edit</button>
  <button type="button" class="btn btn-danger">Delete</button>
</div>
            </td>
        </tr>
        </tbody>
       </table>
    </div>
</template>

<script>
import axios from 'axios'
export default{
    
    name:"X-andrea",
    props:{
        msg: String
    },
    data(){
         return{
            info: null,
            search:""
         }
    },

  mounted()
  {
    axios.get("http://localhost:8080/api/projects")
    .then((res)=>(this.info=res.data));
  },
  methods:{
    find(){
        var x = this.search
        axios.get("http://localhost:8080/api/projects?search="+x)
    .then((res)=>(this.info=res.data));
    }
  


  }
    
    
}
</script>