<template>
  <div id="app"> 
    <!-- 3. component 태그삽입 -->
    <TodoHeader></TodoHeader> 
    <TodoInput></TodoInput>
    <TodoList></TodoList>
    <TodoFooter></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader' //1번 componennt import 파일명 뒤에 .vue 붙여되고, 없어도됨!
import TodoInput from './components//TodoInput'
import TodoList from './components/TodoList'
import TodoFooter from './components/TodoFooter'

export default { 
  components : {  //2번 componentns 메소드에 넣고, export 
    //component 태그명 : component contents(template)
    'TodoHeader': TodoHeader, //TodoHeader의 파일의 내용을 가져와서(import) TodoHeader라는 태그로 만들어줌
    'TodoInput': TodoInput, 
    'TodoList': TodoList,
    'TodoFooter': TodoFooter,

  }
}
</script>

<style>
 body{
   text-align: center;
   background-color: #f6f6f6;
 }
 input{
   border-style: groove;
   width: 200px;  
 }
 button{
   border-style: groove;
 }
 .shadow{
   box-shadow: 5px 10px 10px rgba(0,0,0,0.03);
 }
 i{
   font-size: 0.8rem;
   cursor: pointer;
 }
</style>
