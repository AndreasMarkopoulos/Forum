<template>
  <div class="nav">
    <div class="links">
      <img id="logo" src="../assets/logo.svg" alt="">
      <a @click="toTop">New Post</a>
      <router-link  to="/Feed">Feed</router-link>
      <router-link  to="/myposts">My posts</router-link>
    </div>
    <div class="dropdown">
      <div  class="user" >
        <img src="../assets/user-svgrepo-com.svg" alt="">
        <p>{{username}}</p>
        <p v-if="isadmin" >(admin)</p>
      </div>
      <div class="dropdown-content">
        <router-link class="drop-option" v-if="isadmin" to="/useredit">Edit Users</router-link><br>
        <a class="drop-option" @click="logout" href="">Logout</a>
      </div>
    </div>



  </div>
</template>
<script>
import axios from "axios";

export default {
  data(){
    return{
      isadmin:false,
      username:''
    }
  },
  name:'Header',
  async mounted(){
    let user=localStorage.getItem('userinfo');
    // this.username=await JSON.parse(user).username;
    this.username= JSON.parse(user);
    let res = await axios.get(`http://localhost:3004/user?username=${this.username}`);
    if(res.data[0].admin==='true'){
    this.isadmin=true;}

  },
  methods:{
    toTop(){
      if(this.$route.name!="Feed" || this.$route.name!="Feed#top" ){
        this.$router.push({path:'/Feed'})
      }
      window.scrollTo(0,0);
    },
    logout(){
      localStorage.clear();
      this.$router.push({name:"index"})
    }
  }
}
</script>
<style>
.user{
  min-width: 205px;
  padding-bottom: 0px;
  text-align: center;
  font-size: 17px;
  text-decoration: none;
  display: flex;
  border-radius: 2px;
  background-color: white;
  float: right;
  color: black;
  overflow:hidden;
}

#logo{
  padding-top: 7px;
  overflow: hidden;
  float:left;
  width: 40px;
  height: 40px;
  margin-right:2rem;
}

.user img{
  margin-left: 10px;
  float: left;
  margin-top: 12px;
  width: 30px;
  height: 30px;
}

.nav {
  box-shadow:
    0px 12.1px 23.5px -48px rgba(0, 0, 0, 0.011),
    0px 21.3px 41.6px -48px rgba(0, 0, 0, 0.02),
    0px 27.7px 54.3px -48px rgba(0, 0, 0, 0.028),
    0px 32.4px 62.3px -48px rgba(0, 0, 0, 0.033),
    0px 38.4px 68.2px -48px rgba(0, 0, 0, 0.039),
    0px 50px 79px -48px rgba(0, 0, 0, 0.047),
    0px 69.1px 110.3px -48px rgba(0, 0, 0, 0.058),
    0px 95px 187px -48px rgba(0, 0, 0, 0.07);
  position: fixed;
  z-index: 3;
  top: 0;
  left: 0;
  width: 100%;
  background-color:white;
  overflow:visible;
  padding-top: 5px;
}


.nav a {
  float:left;
  color:black;
  padding: 14px 16px;
  text-align: center;
  font-size: 17px;
  text-decoration: none;
  margin-right: 5px;


}

.nav a:hover{
  background:#ddd;
  color:#333;
}

.user p{
  width: 80px;
  color: black;
  padding-left: 2px;
  margin-left: 0px;
  padding-right: 0px;

}
.user:hover{
  background:#ddd;
  color:#333;
  cursor: pointer;
}

.links a{
  cursor: pointer;
}

.links{
  padding-left:50px;
}

/*drop-down menu*/

.dropdown {
  right: 0;
  margin-right: 30px;
  float: right;
  z-index: 3;
  position: relative;
  display: inline-block;
}

.drop-option{
  margin-left: 4px;
  width: 164px;
}

.dropdown-content {
  z-index: 3;
  margin-top: 56px;
  display: none;
  position: absolute;
  background-color: #f9f9f9;
  width: 205px;
  box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
}

.dropdown-content a:hover {background-color: #f1f1f1}

/* Show the dropdown menu on hover */
.dropdown:hover .dropdown-content {
  display: block;
}

/* Change the background color of the dropdown button when the dropdown content is shown */

</style>

</style>
