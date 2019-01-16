<template>
  <div v-bind:class="{'root':true}">
    <div>
      <h2 v-bind:class="{'h2': true}"> 待办事项 </h2>
    </div>
    <hr>
    <h4>增加待办事项</h4>
    <hr>
    <span>姓名: </span><input required=true type="text" v-model="userName"> <br>
    <br>
    <span>内容: </span><input type="text" v-model="content"><br>
    <br>
    <span>进度: </span><input type="text" v-model="process"><br>
    <br>
    <span>状态: </span><select v-model="status">
    <option value="0">未开始</option>
    <option value="1">进行中</option>
    <option value="2">已完成</option>
  </select>
    <br>
    <br>
    <hr>
    <button @click="add">增加todo</button>
    <br>
    <br>

  </div>
</template>

<script>

  import Axios from "axios";
  export default {
    name: "TodoList",
    data() {
      return {
        todo: [],
        userName: "",
        status: 0,
        content: "",
        process: "",

      }
    },
    methods: {
      getDetail() {
        var userName = this.userName
        var status = this.status
        var api = "/cross/api/v1/" + name + "/" + status + "/getTodo/";
        Axios.get(api).then((response) => {
          console.log(response)
          this.list = response.data;
        }).catch((err) => {
          console.log(err)
        })
      },
      dele(title) {
        this.todo.splice(this.todo.findIndex(this.todo.title === title))
      },
      add() {
        var api = "/cross/api/v1/addTodo/";
        let data = JSON.stringify({
          status: this.status,
          content: this.content,
          userName: this.userName,
          createTime: "2019-01-11T12:00:00"
          //
        });
        Axios({
          method: 'post',
          url: api,
          data: data,
          headers: {'Content-Type': 'application/json'}
        }).then((response) => {
          console.log(response.data)
          if (response.data == true){
            alert("添加成功")
          }
        });


      }
    }

  }
</script>

<style scoped>
  .root {
    background: white;
    position: center;
    width: 80%;
    height: auto;
    padding: 100px;
  }

  .todo {
    width: 400px;
    height: auto;
    background: lightyellow;
  }

  .add {
    color: darkred;
    background: darkkhaki;
  }

  .input_text {
    padding: auto;
    background: lightblue;
    padding-bottom: initial;

  }

  .h2 {
    background: azure;
    color: royalblue;
  }


</style>
