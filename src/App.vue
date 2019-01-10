<template>
  <div id="app">
    <div>
    {{msg}}
    <hr>
    <br>
      <input type="checkbox" >{{users}}<input/>
    <br>
    <button @click="getAllUser">拉取所有用户信息</button>
    </div>
  </div>
</template>

<script>
import Axios from "axios";
export default {
  name: 'App',
  data() {
    return{
       msg: 'hello Vue！',
       users: []
    }
   
  },
  methods:{
    getAllUser: ()=>{
      var api = "/cross/api/v1/user/getAllUser"
      Axios.get(api).then((response)=>{
          console.log(response)
          this.users = response.data
          console.log(this.users)
        }
      ).catch((err)=>{
           console.log(err)
      })


    }
  }
}
</script>

<style>

</style>
