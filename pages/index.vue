<template>
  <div>
    <home-header/>
  <div class="feed-page">
    <div class="homebg">
      <div class="glass post-row" >
        <div>

          <ul class="post" v-for="post in posts.slice().reverse()" :key="post.id">
            <div class="info">
              <img src="../assets/user-svgrepo-com.svg" alt="">
              <p>{{ post.user }}<p/>
            </div>
            <h1>{{ post.title }}</h1>
            <p>{{post.content}}</p>
            <p class="date">{{post.date}}</p>
            <!--      <div class="votes">-->
            <!--        <button class="up-vote" @click="upvote(post.id)"><img src="../assets/upvote.svg"></button>-->
            <!--        <p>{{post.votes}}</p>-->
            <!--        <button class="down-vote" @click="downvote(post.id)"><img src="../assets/downvote.svg"></button>-->
            <!--      </div>-->

          </ul>
        </div>
      </div>
    </div>
  </div>
  </div>
</template>


<script>
import axios from "axios";

export default {
  name: 'index',
  data(){
    return{
      posts:[]
    }
  },
  created() {
    this.dataIn();
  },
  methods: {
    gotoLogin(){
      this.$router.push({name:'Login'})
    },
    gotoSignup(){
      this.$router.push({name:'SignUp'})
    },
    async dataIn(){
      let user = localStorage.getItem('user-info');
      let result = await axios.get('http://localhost:3004/posts/');
      this.posts = result.data;
    }
  },
  mounted(){
    let user=localStorage.getItem('userinfo');
    if(JSON.parse(user)!=null){
      this.$router.push({name:'index'});
    }
  },
}
</script>


<style>
.info{
  display: flex;
}

.info img{
  padding-top: 12px;
  width:25px;
  height: 25px;
  padding-right: 8px;
}

.info p{

  padding-bottom: 10px;
}

.post .date{
  font-size: 14px;
  color: gray;
}

.post h1{
  margin-bottom: 0px;
  font-size: 20px;
}

.post{
  background-color: white;
  padding: 20px;
  margin: 15px;
  border-radius: 5px;
  margin-bottom: 30px;
}

.feed-page{
  background-size: cover;
  margin: 0;
}

.post-row{
  padding-top: 60px;
  width: 60%;
  /*left: 100px;*/
  margin: 0 auto;
}

/*.glass{*/
/*  background-size:cover;*/
/*  background: rgba( 77, 77, 77, 0.1 );*/
/*  box-shadow: 0 8px 32px 0 rgba( 31, 38, 135, 0.37 );*/
/*  backdrop-filter: blur( 10px );*/
/*  -webkit-backdrop-filter: blur( 10px );*/
/*  border: 1px solid rgba( 255, 255, 255, 0.18 );*/
/*}*/

/*.homebg{*/
/*  background-size:cover;*/
/*  background-color:hsla(211,14%,86%,1);*/
/*  background-image:*/
/*    radial-gradient(at 0% 100%, hsla(212,100%,84%,1) 0px, transparent 50%),*/
/*    radial-gradient(at 100% 97%, hsla(279,100%,84%,1) 0px, transparent 50%),*/
/*    radial-gradient(at 87% 33%, hsla(209,100%,83%,1) 0px, transparent 50%);*/
/*}*/

</style>


