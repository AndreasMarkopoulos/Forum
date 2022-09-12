<template>
  <div class="inputs post">
    <h1>Make a new post!</h1>
    <input v-model="title" class="tandp" type="text" id="Title" placeholder="Title (min: 2 characters)"><br>
    <textarea v-model="content" class="tandp" id="post" placeholder="Write your post... (min: 10 characters)"></textarea><br>
    <button class="button-34" @click="submitPost">Post</button>
    <p class="error-msg" v-if="tleng">Post or title is too short!</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: "newpost",
  data() {
    return {
      tleng:false,
      poster: '',
      title: '',
      date: '',
      content: '',
      votes: 0
    }
  },

  methods: {
    async submitPost() {
      if(this.title.length<=2 || this.content.length<=10){
        this.tleng=true;
        return;}
      let usinfo = localStorage.getItem('userinfo');
      this.poster = await JSON.parse(usinfo);
      let res = await axios.post("http://localhost:3004/posts", {
        user: this.poster,
        title: this.title,
        content: this.content,
        date: new Date().toLocaleDateString(),
        votes: this.votes
      });
      if (res.status === 201) {
        this.$root.$refs.feedposts.dataIn();
      }
    }
  }
}
</script>

<style scoped>

.error-msg{
  font-size: 20px!important;
  font-weight: 200!important;
  float: right;
  color: red;
  margin-top:0;
  margin-bottom: 20px;
}

.post h1 {
  margin-bottom: 30px;
  font-weight: bold;
  font-size: 30px;
}

.inputs input {
  font-weight: bold;
  border-radius: 3px;
  border: 3px solid lightgray;
  width: 70%;
  padding: 5px 2px;
}


.inputs textarea {
  resize: none;
  border: 3px solid lightgrey;
  width: 100%;
  margin-top: 20px;
  margin-bottom: 20px;
  padding-bottom: 100px;
}

.post {
  display: block;
  background-color: white;
  padding: 40px;
  padding-top: 10px;
  margin: 15px;
  border-radius: 5px;
  margin-bottom: 30px;
}


/* CSS */
.button-34 {
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
  padding: 8px 18px;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  width: fit-content;
  word-break: break-word;
  border: 0;
}


</style>
