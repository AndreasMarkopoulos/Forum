<template>
  <div class="nav">
    <div class="links">

      <img id="logo"  src="../assets/logo.svg" alt="">
      <router-link  to="/">Home</router-link>
    </div>
      <div  class="user" >
        <img src="../assets/user-svgrepo-com.svg" alt="">
        <router-link  to="/login">Login</router-link>
        <router-link  to="/signup">SignUp</router-link>
      </div>
  </div>
</template>

<script>
export default {
  name: "home-header"
}
</script>

<style scoped>
.user{
  cursor: auto;
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
  cursor: pointer;
  padding-bottom: 7px;
  padding-top: 7px;
  overflow: hidden;
  float:left;
  width: 40px;
  height: 40px;
  margin-right:37rem;
}

.user img{
  cursor: auto;
  padding-right: 10px;
  margin-left: 15px;
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

.links a{
  cursor: pointer;
}

.links{
  padding-left:50px;
}
</style>
