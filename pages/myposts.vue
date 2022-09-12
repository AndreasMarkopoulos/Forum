<template>
  <div>
    <div class="feed-page">
      <custom-header/>
      <div class="homebg">
        <div class="glass post-row" >
          <div>
              <div class="inputs post" v-if="editing">
                <h1>Edit your post</h1>

                <input v-model="editTitle" class="tandp" type="text" id="Title" placeholder="Title (min: 2 characters)"><br>
                <textarea v-model="editContent" class="tandp" id="post" placeholder="Write your post... (min: 10 characters)"></textarea><br>
                <button class="button-22" @click="submitChanges()">Submit</button>
              </div>
            <ul class="post" v-for="mypost in myposts.slice().reverse()" :key="mypost.id">
              <button class="post-action" @click="delPost(mypost.id)" title="delete" ><img src="../assets/trash.svg" /></button>
              <button class="post-action" @click="editPost(mypost.id)" title="edit"><img src="../assets/edit.svg" /></button>
              <div class="info">
                <img src="../assets/user-svgrepo-com.svg" alt="">
                <p>{{ mypost.user }}<p/>
              </div>
              <h1>{{ mypost.title }}</h1>
              <p>{{mypost.content}}</p>
              <p class="date">{{mypost.date}}</p>
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
  name:'myposts',
  data(){
    return{
      editingId:'',
      editTitle:'',
      editContent:'',
      username:'',
      editing:false,
      myposts:[]
    }
  },
  async mounted(){
    this.mypostsdataIn();
    let user=localStorage.getItem('userinfo');
    this.username=JSON.parse(user);
    let res = await axios.get(`http://localhost:3004/user?username=${this.username}`);
  },
  methods:{
    async editPost(id){
      this.editing=!this.editing;
      let result = await axios.get("http://localhost:3004/posts/"+id);
      this.editTitle = result.data.title;
      this.editContent = result.data.content;
      this.editingId=id;
    },
    async delPost(id){
      let result = await axios.delete("http://localhost:3004/posts/"+id);
      if(result.status==200){
        this.mypostsdataIn();
      }
    },
    async submitChanges(){
      let edited= {title: this.editTitle, content:this.editContent}
      let result = await axios.patch("http://localhost:3004/posts/"+this.editingId, edited);
      if(result.status==200){
        this.mypostsdataIn();
      }
      this.editing=false;
    },
    async mypostsdataIn(){
      this.myposts.splice(null,this.myposts.length)
      let user = localStorage.getItem('userinfo');
      this.username=JSON.parse(user);
      let result = await axios.get('http://localhost:3004/posts/');
      for(let i=0; i<result.data.length; i++)
      if(result.data[i].user === this.username){
      this.myposts.push(result.data[i]);}
    }
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

.button-22 {
  background: #5E5DF0;
  border-radius: 999px;
  box-shadow: #5E5DF0 0 10px 20px -10px;
  box-sizing: border-box;
  color: #FFFFFF;
  cursor: pointer;
  font-family: Inter, Helvetica, "Apple Color Emoji", "Segoe UI Emoji", NotoColorEmoji, "Noto Color Emoji", "Segoe UI Symbol", "Android Emoji", EmojiSymbols, -apple-system, system-ui, "Segoe UI", Roboto, "Helvetica Neue", "Noto Sans", sans-serif;
  font-size: 16px;
  font-weight: 700;
  line-height: 24px;
  opacity: 1;
  outline: 0 solid transparent;
  padding: 8px 28px;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  width: fit-content;
  word-break: break-word;
  border: 0;
}


.post-action img{
  height: 25px;
  width: 25px;

}

.post-action{
  cursor: pointer;
  background-color: white;
  border: none;
  margin-right: 10px;
  float: right;

}

.votes p{
  padding-right: 10px;
  padding-left: 15px;
  position: relative;
  bottom:11px;
  font-size: 17px;
  font-weight: bold;
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
  padding-top: 12px
;
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
