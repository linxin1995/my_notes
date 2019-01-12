<template>
  <div v-bind:class="{'root':true}">
    <div>
      <h2 v-bind:class="{'h2': true}"> 待办事项 </h2>
    </div>
    <hr>
    <br>
    <input type="text" v-bind:class="{'input_text': true}" >    <button v-bind:class="{'add':true}" @click="add">增加待办事项</button>
    <br>
    <br>
    <hr>
    <p>进行中</p>
    <br>
    <p v-for="item in todo">{{item}}</p>
    <hr>
    <p>已完成</p>
    <br>

  </div>
</template>

<script>
    import Axios from "axios";

    export default {
        name: "TodoList",
        data(){
          return{
            todo:[]
          }
        },
      methods:{
          getDetail(title){
            var api = "/cross/api/v1/user/getAllUser"
            Axios.get(api).then((response)=>{
              this.list = response.data;
            }).catch((err)=>{
              console.log(err)
            })


            },
          dele(title){
            this.todo.splice(this.todo.findIndex(this.todo.title === title))
          }
      }

    }
</script>

<style scoped>
.root{
  background: white;
  position: center;
  width: 80%;
  height: auto;
  padding: 100px;
}
.todo{
  width: 400px;
  height: auto;
  background: lightyellow;
}
.add{
  color: darkred;
  background: darkkhaki;
}
.input_text{
  padding: auto;
  background: lightblue;
  padding-bottom: initial;

}
  .h2{
    background: azure;
    color: royalblue;
  }



</style>
