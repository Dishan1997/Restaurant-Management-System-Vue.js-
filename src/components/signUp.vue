<template>
<div>
<img class="logo" src="../assets/resto-logo.jpg" />
<h1> Sign Up </h1>
<div class="register">
    <input type="text" v-model="name" placeholder="Enter Name" />
    <input type="text" v-model="email" placeholder="Enter Email" />
    <input type="password" v-model="password" placeholder="Enter Password" />
    <button v-on:click="signUp" > Sign Up </button>
    <p>
     <router-link to="/login">Login</router-link>
    </p>
</div>
</div>
</template>
<script>
import axios from 'axios'
export default {
    name: 'SignUp',
    data(){
        return {
            name: '',
            email: '',
            password: ''
        }
    },
    methods:{
     async signUp(){
       // console.warn("i am inside signUp", this.name, this.email, this.password);
       let result = await axios.post("http://localhost:3000/users", {
        email: this.email,
        name: this.name,
        password: this.password
       });
       console.log(result);
       if(result.status ==201){
        
        localStorage.setItem("User_Info", JSON.stringify(result.data));
        this.$router.push({name: 'Home'});
       console.log("here i am");
       }
     }
    },
    mounted(){
       let user = localStorage.getItem('User_Info');
       if(user){
       this.$router.push({name: 'Home'});
       }
    }
}
</script>
<style>

</style>