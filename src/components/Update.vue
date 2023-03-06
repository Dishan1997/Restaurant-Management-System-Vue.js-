<template>
    <div>
    <Header />
    <h1> Hello User, Welcome on Update Resturant page!</h1>
    <form class="add">
        <input type="text" name="name" placeholder="Enter Resturant Name" v-model="resturant.name"/>
        <input type="text" name="Address" placeholder="Enter Resturant Address" v-model="resturant.Address"/>
        <input type="text" name="contact" placeholder="Enter Resturant Contact Number" v-model="resturant.contact"/>
     <button type="button" v-on:click="updateResturant">Update Resturant</button>
    </form>
 </div>
</template>
<script>
import Header from './Header.vue'
import axios from 'axios'
export default {
    name:'Update',
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
        async updateResturant(){
        //console.log(this.resturant);
        const result = await axios.put("http://localhost:3000/resturant/"+this.$route.params.id,{
            name: this.resturant.name,
            Address: this.resturant.Address,
            contact: this.resturant.contact,
        });
        if(result.status==200){
            this.$router.push({name: 'Home'});
        }
        console.warn(result);
        }
    },
   async mounted(){
       let user = localStorage.getItem('User_Info');
       if(!user){
       this.$router.push({name: 'SignUp'});
       }
       const result = await axios.get('http://localhost:3000/resturant/' + this.$route.params.id);
       console.warn(result);
       this.resturant= result.data;
      // console.warn(this.$route.params.id)
    }
}
</script>