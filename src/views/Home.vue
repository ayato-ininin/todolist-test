<template>
  <div class="home">
    <div class="all">
    <div class="todolist">
      <p>Todolist</p>
      <input type="text">
      <button>追加</button>
    </div>
    </div>
   
  </div>
</template>

<script>

export default {
  name: 'Home',
}
</script>

<style scoped>
.todolist{
  text-align: center;
  display: inline-block;
  background-color: #fff;
  color: black;
  width:700px;
  height: 250px;
  border-radius: 15px;

}
.all{
  text-align: center;
  margin: auto 0;
  margin-top:250px;

}
p{
  color: black;
}
</style>
