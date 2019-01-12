<template>
  <div id="app">
    <vue-todo></vue-todo>
    <div>
    <hr>
    <br>
    <br>
    </div>
  </div>
</template>

<script>
import Axios from "axios";
// 引入组件
import TodoList from "./components/TodoList";
export default {
  name: 'App',
  data() {
    return{
       msg: 'hello Vue！',
       list: ['asdfas','asdfadg','asdgag'],
       flag: true
    }
  },
  methods:{
    getAllUser(){
      this.msg = "获取数据中。。。。"
      var api = "/cross/api/v1/user/getAllUser"
      Axios.get(api).then((response)=>{
        this.list = response.data;
        }).catch((err)=>{
           console.log(err)
      })


    }
  },
  mounted() {
    console.log("生命周期函数mounted 会在页面加载时执行 包括刷新")
  },
  components:{
    // 手动挂在组件
    "vue-todo": TodoList
  }

}
</script>

<style>
 .top{
   color: red;
   background: black;
 }

</style>
