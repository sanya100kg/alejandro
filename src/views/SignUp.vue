<template>
    <div class="page-signup">
        <h1 class="title">Sign UP</h1>
        <div class="columns">
            <div class="columns is-4 is-offset-4">
                

                <form @submit.prevent="submitForm">
                    <div class="field">
                        <label>E-mail</label>
                        <div class="control">
                            <input type="email" name="username" class="input" v-model="username">
                        </div>
                    </div>

                    <div class="field">
                        <label>Password</label>
                        <div class="control">
                            <input type="password" name="password" class="input" v-model="password">
                        </div>
                    </div>

                    <div class="notification is-danger" v-if="errors.length">
                       <p v-for="error in errors" v-bind:key="error"> {{ error }} </p>
                    </div>

                    <div class="field">
                        <div class="control">
                            <button class="button is-success">Sign UP</button>
                        </div>
                    </div>

                </form>
            </div>
        </div>
    </div>

</template>

<script>
import axios  from 'axios'
export default{
    name:'SignUp',
    data(){
        return{
            username:'',
            password:'',
            errors:[],
        }
    },
    methods:{
        submitForm(e){
            const formData={
                username:this.username,
                password:this.password
            }
            axios
                .post("http://127.0.0.1:8000/api/v1/users/",formData)
                .then(response=>{
                    console.log(response)

                    this.$router.push('/log-in')
                })
            .catch(error=>{
                this.errors=[]
                if(error.response){
                        console.log('huis')
                        console.log(Object.keys(error.response.data).length)
                        
                        for (const property in error.response.data){
                            console.log(error.response.data[property])
                        if(Object.keys(error.response.data).length==1){
                            
                            this.errors.push(`${property}: ${error.response.data[property]}`)
                        }
                        else if(Object.keys(error.response.data).length==0){

                        }
                        else{
                            this.errors.push(`${property}: ${error.response.data[property]}`)
                        }                      
                        }
                    }    
                                  
            })
        }
    }
}
</script>