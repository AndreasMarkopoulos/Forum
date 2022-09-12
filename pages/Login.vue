<template>
  <div>
    <home-header/>
  <div class="def-background">
    <div class="register-form">
      <h1>Login</h1>
      <input type="text" v-model="username" placeholder="Username"/>
      <input type="password" v-model="password" placeholder="Password"/>
      <div v-if="nouser" class="wrong-data" >Wrong username or password</div><br>
      <button @click="login" >LOGIN</button><br>
      <a class="signup" @click="goToSignUp">Sign up</a>
    </div>

  </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: "Login",
  data(){
    return{
      username:'',
      email:'',
      password:'',
      nouser:false
    }
  },
  mounted(){
    let user=localStorage.getItem('userinfo');
    if(user){
      this.$router.push({name:'Feed'});
    }
  },
  methods:{
    goToSignUp(){
      this.$router.push('signup');
    },
    async login(){
      let res = await axios.get(`http://localhost:3004/user?username=${this.username}`);
      const users = res.data;

      if (users.length === 0) {
        this.nouser = true;
        return;
      }

      const user = users[0];
      if (user.password === this.password) {
          this.nouser=false;
          localStorage.setItem("userinfo",JSON.stringify(this.username));
          this.$router.push({name:'Feed'})
      }
      else {
        this.nouser = true;
      }



      // console.warn(res.status);
      // if(res.status===200 && res.data.length>0){
      //   this.nouser=false;
      //   localStorage.setItem("userinfo",JSON.stringify(res.data[0]));
      //   this.$router.push({name:'Feed'})
      // }
      // else{
      //   this.nouser=true;
      //   return}
    }
}}

</script>

<style scoped>

.signup{
  cursor:pointer;
  color:hsla(211,100%,38%,1);
  font-weight: bold;
}

.def-background {
  left: 0;
  background-size:cover;
  width: 100%;
  margin: auto 0px;
  height: 100vh;
  background-color:hsla(211,14%,86%,1);
  background-image:
    radial-gradient(at 0% 100%, hsla(212,100%,84%,1) 0px, transparent 50%),
    radial-gradient(at 100% 97%, hsla(279,100%,84%,1) 0px, transparent 50%),
    radial-gradient(at 87% 33%, hsla(209,100%,83%,1) 0px, transparent 50%);
}

.wrong-data{

  color: red;
  margin-top:0;
  margin-bottom: 20px;
}

.register-form h1{
  margin-bottom: 50px;
}

.register-form{
  padding: 28px;
  background-color: white;
  text-align: center;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
  box-shadow:
    0px 17.9px 1.9px rgba(0, 0, 0, 0.015),
    0px 32.3px 4.3px rgba(0, 0, 0, 0.027),
    0px 42.8px 7.7px rgba(0, 0, 0, 0.033),
    0px 50.8px 12.8px rgba(0, 0, 0, 0.038),
    0px 60.9px 21.2px rgba(0, 0, 0, 0.045),
    0px 77.3px 37px rgba(0, 0, 0, 0.056),
    0px 100px 80px rgba(0, 0, 0, 0.07)
;


}

.register-form input {
  width: 350px;
  display: block;
  margin-bottom: 50px;
  padding: 18px;

}

.register-form button{
  border-radius: 6px;
  font-weight: bold;
  letter-spacing: 2px;
  margin-bottom: 15px;
  cursor: pointer;
  padding: 15px;
  width: 175px;
  background-color: #005dc6;
  border: none;
  color: white;
}

.register-form button:hover{
  cursor: pointer;
  padding: 15px;
  width: 175px;
  background-color: #0077ff;
  border: none;
}

</style>
