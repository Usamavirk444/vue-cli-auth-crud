<template>
    <img class="logo" src="@/assets/resto-logo.png" alt="">
    <h1>Login</h1>
    <div class="login">
        <input type="text" v-model="email" placeholder="Enter Email">
        <input type="password" v-model="password" placeholder="Enter Password">
        <button @click="login">Login</button>
        <p>
            <router-link to="/sign-up">Sign Up</router-link>
        </p>
    </div>
</template>

<script>
import axios from "axios";
export default {
    name:'LogIn',
    data(){
        return{
            email:'',
            password:''
        }
    },
    methods:{
        async login(){
            let result = await axios.get(`http://localhost:3000/users?email=${this.email}&password=${this.password}`)
            console.log(result.data);
            if(result.data){
                localStorage.setItem('user-info',JSON.stringify(result.data[0]));
                this.$router.push({name:'HomePage'});
            }
            else{
                alert('Invalid Credentials');
            }
        }
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if(user){
            this.$router.push({name:'HomePage'});
        }
    },
}
</script>

<style lang="scss" scoped>

</style>