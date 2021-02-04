<template>
  <div class="home">
    <div class="all">
      <div class="todolist">
        <div class="title">
        <p>Todo list</p>
        </div>
        <div class="content">
        <input type="text" class="conts" v-model="todo">
        <button class="btn1" @click="send">追加</button>
     </div>
     <div v-for="(todo,index) in todolist" :key="index">
      <div class="content">
        <input type="text" class="cont" v-model="todo.data.todo">
        <div class="btn">
        <button class="btn2" @click="upd(todo.data.todo,index)">更新</button>
        <button class="btn3" @click="del(index)">削除</button>
        </div>
      </div>
      </div>
    </div>
  


    </div>
   
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: 'Home',
  data(){
    return{
      todo:"",
      todolist:[],
    };
  },
  methods:{
    send(){
      if(this.todo===""){
        alert("内容を入力してください");
      }else{
        axios.post("https://frozen-headland-03525.herokuapp.com/api/todos",{
          todo:this.todo,
        })
        .then((response)=>{
          console.log(response);
          this.todo="";
          this.$router.go({
            path:this.$router.currentRoute.path,
            force:true,
          });
        });
      }
    },
    async getTodos(){
      let data=[];
      const todos =await axios.get(
        "https://frozen-headland-03525.herokuapp.com/api/todos"
      );
      for (let i =0; i<todos.data.data.length;i++){
        await axios.get("https://frozen-headland-03525.herokuapp.com/api/todos/" +todos.data.data[i].id)
      
      .then((response)=>{
        data.push(response.data);
      });
      }
      this.todolist=data;
      console.log(this.todolist);
   },
   del(index){
     axios.delete(
       "https://frozen-headland-03525.herokuapp.com/api/todos/" +this.todolist[index].data.id
     );
     
  },
  upd(newtodo,index){
    const newdata ={
      todo:newtodo,
    };
    axios.put("https://frozen-headland-03525.herokuapp.com/api/todos/" + this.todolist[index].data.id,newdata
    )
    .then((response)=>{
       console.log(response);
       this.$router.go({
         path:this.$router.currentRoute.path,
         force:true,
     });
     });

  },
  },
  created(){
    this.getTodos();
  },
  
};
</script>

<style scoped>
.todolist{
  text-align: left;
  display: inline-block;
  background-color: #fff;
  color: black;
  width:50%;
  height:auto;
  border-radius: 15px;
  padding: 25px;
}
.all{
  text-align: center;
  margin:0 auto;
  margin-top:180px;

}
input{
  color: black;
  border:1px solid #d3d3d3;
  border-radius: 5px;
}
.content{
  display: flex;
  justify-content: space-between;
  margin: 15px 25px;
}
p{
  color: black;
}
.conts{
  width:70%;
  height: 28px;
}
.cont{
  width: 30%;
  height: 23px;

}
.title{
  font-size: 27px;
  font-weight: bold;
  margin: 15px;
}
.btn1{
  color: #ff00ff;
  border:2px solid #ff00ff;
  font-weight: bold;
  border-radius: 5px;
  padding: 10px 15px;
  background-color: #fff;
}
.btn1:hover{
  cursor: pointer;
  background-color: #ff00ff;
  color: #fff;
  transition: 0.3s;
}
.btn2{
  color: #ffa500;
  border:2px solid #ffa500;
  font-weight: bold;
  border-radius: 5px;
  padding: 10px 15px;
  background-color: #fff;
  margin-right: 7px;
}
.btn2:hover{
  cursor: pointer;
  background-color:  #ffa500;
  color: #fff;
  transition: 0.3s;
}
.btn3{
  color:#7fffd4;
  border:2px solid #7fffd4;
  font-weight: bold;
  border-radius: 5px;
  padding: 10px 15px;
  background-color: #fff;
}
.btn3:hover{
  cursor: pointer;
  background-color: #7fffd4;
  color: #fff;
  transition: 0.3s;
}
</style>
