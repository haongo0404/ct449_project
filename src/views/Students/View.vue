<template>
    <div class="container">
        <div class="card">
            <div class="card-header">
                <h4>Students
                    <RouterLink to="/students/create" class="btn btn-primary float end">
                        ADD
                    </RouterLink>
                </h4>
            </div>
            <div class="card-body">
                <table class="table table-bordered">
                <thead>
                    <tr>
                        <td>ID</td>
                        <td>address</td>
                        <td>email</td>
                        <td>name</td>
                        <td>phone</td>
                        <td>action</td>
                    </tr>
                </thead>
                <tbody v-if="this.contacts.length > 0">
                    <tr v-for="(contacts,index) in this.contacts" :key="index">
                        <td>{{ contacts._id }}</td>
                        <td>{{ contacts.address }}</td>
                        <td>{{ contacts.email }}</td>
                        <td>{{ contacts.name }}</td>
                        <td>{{ contacts.phone }}</td>
                        <td><RouterLink :to="{ path: '/students/' +contacts._id+'/edit'}" class="btn btn-success float end">
                        Edit
                    </RouterLink>
                    <button type="button" class="btn btn-danger">Delete</button>
                </td>
                    
                    </tr>
                </tbody>
                <tbody v-else>
                    <tr>
                        <td colspan="6">
                            Loading...
                        </td>
                    </tr>
                </tbody>
                </table>
            </div>
        </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios'
  export default {
    name:'contacts',
    data(){
        return{
            contacts:[]
        }
    },
    mounted(){
        console.log("day");
        this.getStudents();
    },
    methods:{
        getStudents(){
            axios.get('http://localhost:3000/api/contacts').then( res=>{
                this.contacts=res.data
                console.log(this.contacts);
            })
        }
    }
  }
</script>