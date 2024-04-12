<template>
     <RestoHeader />
    <h1>Hello Welcome on Update Restaurant page</h1>
    <div>
        <form action="">
            <input type="text" name="name" v-model="restaurant.name" placeholder="Enter Name">
            <input type="text" name="address" v-model="restaurant.address" placeholder="Enter Address">
            <input type="text" name="contact" v-model="restaurant.contact" placeholder="Enter Contact No">
            <button type="button" @click="updateResturant">Submit</button>
        </form>
    </div>
</template>

<script>
import RestoHeader from "./RestoHeader.vue";
import axios from "axios";
export default {
    name:"UpdateRestaurant",
    data(){
        return{
            restaurant:{
               name:'', 
               address:'', 
               contact:''
            },
            }
    },
    methods: {
       async updateResturant(){
            let result = await axios.put('http://localhost:3000/restsurants/'+this.$route.params.id,{
                name:this.restaurant.name,
                address:this.restaurant.address,
                contact:this.restaurant.contact,
            });
            console.log(result);
            

        }
    },
    async mounted(){
            let reponse = await axios.get('http://localhost:3000/restsurants/'+this.$route.params.id)
            if(reponse.data){
                this.restaurant = reponse.data
            }else{
                this.$router.push({name:'Home'})
            }
    },
    components:{RestoHeader}
}
</script>

<style>
form {
  width: 300px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

input[type="text"] {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button[type="button"] {
  width: 100%;
  padding: 10px;
  background-color: #4CAF50;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button[type="button"]:hover {
  background-color: #45a049;
}
</style>