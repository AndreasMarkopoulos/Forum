<template>
  <div class="feed-page">
    <custom-header/>
  <div class="homebg">
    <div class="glass post-row" >
      <feedposts />
    </div>
  </div>
  </div>
</template>

<script>
export default {
  name: "Feed",
  data(){
    return{
      name:''
    }
  },
  mounted(){
    let user = localStorage.getItem('userinfo');
    if(!user){
      this.$router.push({name:"index"});
    }
  }
}
</script>

<style>



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

