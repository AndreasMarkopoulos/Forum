<template>
  <div>
    <newpost/>
  <div>

    <ul class="post" v-for="post in posts.slice().reverse()" :key="post.id">
      <button class="del-post" @click="delPost(post.id)" v-if="isadmin"><img src="../assets/trash.svg" /></button>
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
</template>

<script>
import axios from "axios";
export default {
  name:'feedposts',
  data(){
    return{
      upvoted:false,
      downvoted:false,
      posts:[],
      isadmin:false
    }
  },
  created() {
    this.$root.$refs.feedposts = this;
    this.dataIn();
  },
  async mounted(){
    let user=localStorage.getItem('userinfo');
    // this.username=await JSON.parse(user).username;
    this.username=JSON.parse(user);
    let res = await axios.get(`http://localhost:3004/user?username=${this.username}`);
    if(res.data[0].admin==='true'){
      this.isadmin=true;}
  },
  methods:{
    async delPost(id){
      let result = await axios.delete("http://localhost:3004/posts/"+id);
      if(result.status==200){
        this.dataIn();
      }
    },

    async dataIn(){
      let user = localStorage.getItem('user-info');
      let result = await axios.get('http://localhost:3004/posts/');
      this.posts = result.data;
    },
    //
    // upvote(id){
    //   this.upvoted=!this.upvoted;
    //   this.downvoted=false;
    //   this.voting(id);
    // },
    // downvote(id){
    //   this.downvoted=!this.downvoted;
    //   this.upvoted=false;
    //   this.voting(id);
    // },
    // async voting(id){
    //   let res = await axios.get('http://localhost:3004/posts/'+id);
    //   let count=parseInt(res.data.votes);
    //   if(this.upvoted){
    //     count = parseInt(res.data.votes) + 1;
    //   }
    //   else if(this.downvoted){
    //     count = parseInt(res.data.votes) - 1;
    //   }
    //   console.log(count);
    //   let result = await axios.patch("http://localhost:3004/posts/"+id, {votes:count});
    //   // if(result.status===200){
    //   //   this.dataIn();}
    // }


  }
}

</script>



<style scoped>

.votes{

  display: flex;
}

.del-post img{
  height: 25px;
  width: 25px;

}

.del-post{
  position: absolute;
  right: 35px;

}

.votes p{
  padding-right: 10px;
  padding-left: 15px;
  position: relative;
  bottom:11px;
  font-size: 17px;
  font-weight: bold;
}

button{
  background-color: white;
  cursor: pointer;
  border: none;
  border-radius: 3px;
  width: 30px;
  height: 30px;
  padding: 3px;
}
button img{
  margin:0 auto;
  position: relative;
  width: 30px;
  height: 30px;
  padding-bottom: 2px;
}
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
</style>
