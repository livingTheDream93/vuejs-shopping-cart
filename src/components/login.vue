<template>
     <v-container fluid fill-height id="container-background">
      <v-layout justify-center align-center style="min-height:95vh">
        <v-flex xs12 md4 sm6>
          <v-card hover dark >
            <v-toolbar >
              <v-toolbar-title>Login</v-toolbar-title>
            </v-toolbar>
            <v-card-text :style="bgTrans">
              <v-form ref="form" v-model="valid" lazy-validation>
               
                <v-text-field
                  v-model="email"
                  :rules="emailRules"
                  label="E-mail"
                  required
                ></v-text-field>
                <v-text-field
                  v-model="password"
                  :rules="passwordRules"
                  label="password"
                  required
                  type="password"
                >

                </v-text-field>
                <v-btn
                  :disabled="!valid"
                  @click="submit"
                >
                  submit
                </v-btn>
              </v-form>
            </v-card-text>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container> 
</template>

<script>
import axios from 'axios'
export default {
    name:'login',
     data: () => ({
      valid: true,
     
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid'
      ],
      password: '',
      passwordRules: [
        v => !!v || 'Password is required',
        v => (v && v.length >= 4) || 'Password should be greater than 6 characters'
      ],
      bgTrans:{
          color:'black',
          backgroundColor:'rgba(255,255,255,0.1)'
      }
     
    }),
    methods: {
      
      submit () {
        if (this.$refs.form.validate()) {
          axios({
            method:'post',
            url:'http://18.218.116.59:3030/api/auth/login',
            data:{
              "email": this.email,
              "password": this.password
            },
            headers:{
              "Content-Type":"application/json"
            }
          })
          .then((response) =>{
            console.log(response)
            if(response.status != 200) {
              console.log('error logging in user')
            } else {
              //Setting token and email in local storage
              console.log('Bingo! Logged In')
              localStorage.setItem('token', response.data.data.token);
              localStorage.setItem('email', response.data.data.email);
              console.log(this)
            }
          }).then((res)=>{
            this.$router.push('/products')
          }).catch((e)=>{
            console.log(e);
            
          })
         }
      }
      
     },
     props : {
         source : String
     }
}
</script>

<style scoped>

#container-background{
    background: linear-gradient(0deg, rgba(255,255,255,0.6), rgba(90, 32, 6, 0.5)), url('../assets/books.jpg');
    background-size: cover;
    background-color: rgba(0,0,0,0.6)
    
}


</style>

<style>

</style>
