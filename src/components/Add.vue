<template>
    <div>
    <Header />
    <h1> Hello User, Welcome on Add Resturant page!</h1>
    <form class="add">
        <input type="text" name="name" placeholder="Enter Resturant Name" v-model="resturant.name"/>
        <input type="text" name="Address" placeholder="Enter Resturant Address" v-model="resturant.Address"/>
        <input type="text" name="contact" placeholder="Enter Resturant Contact Number" v-model="resturant.contact"/>
     <button type="button" v-on:click="addResturant">Add New Resturant</button>
    </form>
 </div>
</template>
<script>
import Header from './Header.vue'
import axios from 'axios'
export default {
    name:'Add',
    components:{
        Header
    },
    data(){
   return {
     resturant:{
        name:'',
        Address:'',
        contact:''
     }
   }
    },
    methods:{
      async addResturant(){
        console.log(this.resturant);
        const result = await axios.post("http://localhost:3000/resturant",{
            name: this.resturant.name,
            Address: this.resturant.Address,
            contact: this.resturant.contact,
        });
        if(result.status==201){
            this.$router.push({name: 'Home'});
        }
        console.warn(result);
      }
    },
   mounted(){
       let user = localStorage.getItem('User_Info');
       if(!user){
       this.$router.push({name: 'SignUp'});
       }
    }
}
</script>