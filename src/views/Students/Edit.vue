<template>
    <div class="container mt-5">
        <div class="card">
            <div class="card-header">
                <h4>EDIT</h4>
            </div>
            <div class="card-body">
                <ul class="alert alert-warning" v-if="Object.keys(this.errorList).length > 0">
                    <li class="mb-0 ms-3" v-for="(error,index) in this.errorList" :key="index" >
                        {{ error[0] }}
                    </li>
                </ul>
                <div class="mb-3">
                    <label for="">Adress</label>
                    <input type="text" class="form-control" v-model="model.contacts.address" name="" id="" />
                </div>
                <div class="mb-3">
                    <label for="">email</label>
                    <input type="text" class="form-control" v-model="model.contacts.email" name="" id="" />
                </div>
                <div class="mb-3">
                    <label for="">name</label>
                    <input type="text" class="form-control" v-model="model.contacts.name" name="" id="" />
                </div>
                <div class="mb-3">
                    <label for="">Phone</label>
                    <input type="text" class="form-control" v-model="model.contacts.phone" name="" id="" />
                </div>
                <div class="mb-3">
                    <button type="button" @click="updateStudent" class="btn btn-primary">Luu</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios';
export default {
    name: 'studentsEdit',

    data() {
        return {
            studentId:'',
            errorList: '',
            model: {
                contacts: {
                    address: '',
                    email: '',
                    name: '',
                    phone: ''
                }
            }
        }
    },
    mounted(){
        //console.log(this.$route.params.id);
        this.studentId=this.$route.params.id;
        this.getStudentData(this.$route.params.id)
    },
    methods:{
        getStudentData(studentId){
            axios.get(`http://localhost:3000/api/contacts/${studentId}`).then(res=>{
                console.log(res.data)
                this.model.contacts=res.data
            });
        },
        updateStudent() {
            var mythis=this;
            axios.put(`http://localhost:3000/api/contacts/${this.studentId}`, this.model.contacts)
            .then(res => {
                console.log(res.data)
                alert(res.data.message);
                this.errorList='';
            })
            .catch(function (error) {
                    if(error.response) {
                        if(error.response.status==422){
                            mythis.errorList=error.response.data.errors;
                        }
                        if(error.response.status==404){
                            mythis.errorList=error.response.data.message;
                        }
                    } else if (error.request) {
                        console.log(error.request);
                    } else {
                        // Something happened in setting up the request that triggered an Error
                        console.log('Error', error.message);
                    }
            })
        }
    }
}
</script>