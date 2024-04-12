<template>
    <div class="nav">
        <router-link to="/">Home</router-link>
        <router-link to="/create-restaurant">Add Restaurant</router-link>
        <router-link to="/update-restaurant">Update Restaurant</router-link>
        <a href="#" @click="logout">Logout</a>
    </div>
</template>

<script>
export default {
    name:'RestoHeader',
    methods:{
        logout(){
            localStorage.clear();
            this.$router.push({name:'LogIn'});
        }
    }
}
</script>

<style>
.nav{
    background-color: #333;
    overflow: hidden;

}

.nav a {
    float: left;
    color: #f2f2f2;
    padding: 14px;
    text-decoration: none;
    text-align: center;
    font-size: 17px;
}

.nav a:hover{
    background:#ddd ;
    color: #333;
}

</style>