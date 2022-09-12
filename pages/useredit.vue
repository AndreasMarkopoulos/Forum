<template>
    <div>
      <custom-header/>
      <div class="homebg">
        <div class="userlist glass">
          <table>
            <tr class="tableTitles">
              <td>Id</td>
              <td>Username</td>
              <td>Email</td>
              <td>Is admin</td>
              <td>Actions</td>
            </tr>
            <tr v-for="item in users" :key="item.id">
              <td>{{item.id}}</td>
              <td>{{item.username}}</td>
              <td>{{item.email}}</td>
              <td>{{item.admin}}</td>
              <td>
                <button class="action-button" @click="delUser(item.id)">Ban user</button>
                <button class="action-button" @click="demote(item.id)">Demote admin</button>
                <button class="action-button" @click="makeAdmin(item.id)">Make admin</button>


              </td>
            </tr>

          </table>
        </div>
      </div>
    </div>

</template>

<script>
import axios from "axios";
export default {
  name:'useredit',
  data(){
    return{
      isadmin:false,
      users:[]
    }
  },
  async mounted() {
    let user=localStorage.getItem('userinfo');
    // this.username=await JSON.parse(user).username;
    this.username= JSON.parse(user);
    let res = await axios.get(`http://localhost:3004/user?username=${this.username}`);
    if(res.data[0].admin==='true'){
      this.isadmin=true;}
  }
  ,
  created() {
    this.dataIn();
},
  methods:{

    async makeAdmin(id){
      let result = await axios.patch("http://localhost:3004/user/"+id, {admin:'true'});
      if(result.status==200){
        this.dataIn();
      }
    },
    async demote(id){
      let result = await axios.patch("http://localhost:3004/user/"+id, {admin:'false'});
      if(result.status==200){
        this.dataIn();
      }
    },

    async delUser(id){
      let result = await axios.delete("http://localhost:3004/user/"+id);
      if(result.status==200){
        this.dataIn();
      }
    },
    async dataIn(){
      let user = localStorage.getItem('user-info');
      let result = await axios.get('http://localhost:3004/user/');
      this.users = result.data;
    }

  }
}

</script>

<style>
td {

  text-align: center;
  width: 20%;
  height: 40px;
  border-right: none;
  border-left: none;
  padding:10px;
}

tr{
  background:rgba( 255, 255, 255, 0.3 );
  box-shadow: 0 8px 8px 0 rgba( 31, 38, 135, 0.37 );
  backdrop-filter: blur( 4px );
  -webkit-backdrop-filter: blur( 4px );
  border-radius: 0;
  border: 1px solid rgba( 255, 255, 255, 0.3 );;
}

table {

  padding-left: 20px;
  padding-right: 20px;
  align-items: center;
  width:100%;
  border-spacing: 0 10px;

}

.userlist{
  padding-top: 60px;
  width: 60%;
  /*left: 100px;*/
  margin: 0 auto;
}

.tableTitles{
  width: 100%;
  font-weight: bold;
}

button{
  width: 100px;
  margin-bottom: 5px;
}

.action-button{
  cursor: pointer;
  font-size: .8rem;
  margin-left: 1rem;
  background: rgba(171, 99, 99, 0.1);
  border: 1px solid black;
  padding: .3rem;
  border-radius: 2px;
  color:black;
}

.action-button:hover{
  box-shadow: inset 0 2px 2px 0 rgba( 31, 38, 135, 0.37 ) ;
}


</style>
