<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo"> 
    <!-- v-keyup:enter 아님 -->
    <span class="addContainer" v-on:click="addTodo">
      <i class="fas fa-plus-circle addBtn"></i>
    </span>
  </div>
</template>

<script>
export default {
  // 데이터는 함수형, 리턴객체형
  data: function(){
    return{
      newTodoItem: ''
    }
  },
  methods:{
    addTodo: function (){
      //console.log(this.newTodoItem);
      //저장하는 로직(key, value)
      //객체 생성 -> check버튼 사용위하여 
      if(this.newTodoItem !== ''){ //값이 있으면
      var obj = {completed: false, item: this.newTodoItem}; 
      //JOSN.stringify 자바스크립트 객체를 string으로 변환
      // JSON.stringify() 는 javascript 객체를 string값으로 변환시킴
      //그 이유: localstorage는 객체 출력이 안되고, string text값만 출력됨
      // localStorage.setItem(this.todoItems, this.todoItems)으로 했다가
      // todoList에서 checkbox의 toggle 메소드 사용을 위해 아래로 변경
      // obj라는 객체에 담아주고, 아래 localstorage value값을 string으로 변환하여 입력
      localStorage.setItem(this.newTodoItem, JSON.stringify(obj));
      this.clearInput();
      }
    },
    clearInput: function (){
      this.newTodoItem=''; 
    }
  }
}
</script>

<style scoped>
  input:focus {
    outline: none;
  }
  .inputBox {
    background: #fff;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
  }
  .inputBox input {
    border-style: none;
    font-size: 0.9rem;
  }
  .addContainer {
    float: right;
    background: linear-gradient(to right, #6478fb, #8763fb);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
  }
  .addBtn {
    color: #fff;
    vertical-align: middle;
  }
</style>