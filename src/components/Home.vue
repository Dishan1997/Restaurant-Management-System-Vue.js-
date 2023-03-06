<template>
    <div>
    <Header />
    <h1> Hello {{ name }}, Welcome on Home page!</h1>
    <table border="1">
        <tr>
        <td>Id</td>
        <td>Name</td>
        <td>Contact</td>
        <td>Adrress</td>
        <td>Actions</td>
       </tr>
        <tr v-for="item in resturant" :key ="item.id">
        <td>{{ item.id }}</td>
        <td>{{ item.name }}</td>
        <td>{{ item.contact }}</td>
        <td>{{ item.Address }}</td>
        <td>
        <router-link :to="'/update/' + item.id">Update</router-link>
        <button v-on:click="deleteResturant(item.id)">Delete</button>
        </td>
        </tr>
    </table>
 </div>
</template>
<script>
import Header from './Header.vue'
import axios from 'axios'
export default {
    name:'Home',
    data(){
        return{
            name:'',
            resturant:[],
        }
    },
    components:{
        Header
    },
    methods:{
     async deleteResturant(id){
        let result =await axios.delete("http://localhost:3000/resturant/"+ id);
        if(result.status==200){
         this.loadData();
        }
      },
      async loadData(){
        let user = localStorage.getItem('User_Info');
       this.name = JSON.parse(user).name;
       if(!user){
       this.$router.push({name: 'SignUp'});
       }
       let result =await axios.get("http://localhost:3000/resturant");
       console.warn(result);
       this.resturant = result.data;
      }
    },
    async mounted(){
       this.loadData();
    }
}
</script>
<style>
 td{
    width: 160px;
    height: 40px;
 }
 button{
    margin-left: 5px;
    cursor: pointer;
 }
 button:hover{
    background-color:red;
 }
 table{
    margin-left: 18%;
 }
</style>