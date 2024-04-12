<template>
    <RestoHeader />
    <h1>Hello {{ user }} Welcome on home page</h1>
    <table>
        <thead>
            <tr>
                <th>sr #</th>
                <th>Name</th>
                <th>Address</th>
                <th>Contact no</th>
                <th>Actions</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(resturant, index) in restsurants" :key="resturant.id">
                <td>{{ index + 1 }}</td>
                <td>{{ resturant.name }}</td>
                <td>{{ resturant.address }}</td>
                <td>{{ resturant.contact }}</td>
                <td><router-link :to="'update-restaurant/' + resturant.id">Edit</router-link></td>
                <td><button type="button" @click="deleteResturant(resturant.id)">delete</button></td>
            </tr>
        </tbody>
    </table>
</template>

<script>
import RestoHeader from './RestoHeader.vue';
import axios from 'axios';

export default {
    name: 'HomePage',
    components: {
        RestoHeader
    },
    data() {
        return {
            user: '',
            restsurants: []
        };
    },
    async mounted() {
        this.loadData();
    },
    methods: {
        async deleteResturant(id) {
            try {
                const response = await axios.delete("http://localhost:3000/restsurants/" + id);
                this.loadData();
                console.log(response);
            } catch (error) {
                console.error(error);
            }
        },
        async loadData() {
            let userInfo = localStorage.getItem('user-info');
            if (userInfo) {
                try {
                    this.user = JSON.parse(userInfo).name.toUpperCase();
                } catch (error) {
                    console.error('Failed to parse user info:', error);
                    this.$router.push({ name: 'SignUp' });
                }
            } else {
                this.$router.push({ name: 'SignUp' });
            }

            let result = await axios.get("http://localhost:3000/restsurants");
            if (result.data) {
                this.restsurants = result.data
            }
        }
    },
}
</script>

<style scoped>
table {
    width: 100%;
    border-collapse: collapse;
}

th {
    background-color: #f2f2f2;
    padding: 10px;
    text-align: left;
}

td {
    border-bottom: 1px solid #ddd;
    padding: 10px;
    text-align: left;
}

tr:nth-child(even) {
    background-color: #f2f2f2;
}
</style>