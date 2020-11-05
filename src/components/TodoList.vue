<template>
  <div>
      <ul>
        <!-- 중요 v-for instance특징, 반복문구의 index를 알려준다 -->
        <!-- 클릭 remove event 위하여 todoItem, index(삭제할 해당건)를 메소드에 넘겨준다 -->
        <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.item" class="shadow">
          <i class="fas fa-check checkBtn" v-bind:class="{checkBtnCompleted: todoItem.completed}" 
          v @click="toggleComplete(todoItem, index)"></i>
          <!-- 중요 v-bind 클래스 기존의 html 속성중 todoItem.completed값이 true면 textCompleted class가 동작한다 ->class on/off-->
          <span v-bind:class="{textCompleted: todoItem.completed}">{{todoItem.item}} </span>
          <!-- {{todoItem}}으로 출력시 { "completed": false, "item": "dsdasa" } 로 나옴 -> .item 속성접근 -->
          <!-- todoItem,index를 인자로 넣어 넘긴다 -->
          <span v-on:click="removeItem(todoItem, index)" class="removeBtn"><i class="far fa-trash-alt"></i></span>
        </li>
      </ul>
    </div>
</template>

<script>
export default {
  data: function (){
    return{ 
      //localstorage에서 가져올 담는 공간
      todoItems: []
    }
  },
  //vue lifecycle 중 instance가 생성되자마다 호출되는 lifecycle hook
  created: function(){
     if(localStorage.length > 0){
       for(var i = 0; i < localStorage.length; i++){
         if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
          //localstorage key값을 getItem하면 value가 output됨
          //value가 json.stringify(tooinput 파일)에서 string type -> 객체형태로 변환해줘야함
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
         //this.todoItems.push(localStorage.key(i));           
         }
       }
     }
  },
  methods:{
      removeItem: function (todoItem, index){
      //console.log(todoItem,index);
      //localstorage에서 지워주는 로직
       localStorage.removeItem(todoItem);
       //화면에서 빼기
       this.todoItems.splice(index, 1);
      },
      toggleComplete: function (todoItem, index) { //eslint-disable-line no-unused-vars
        todoItem.completed = !todoItem.completed;
        //localstorage data 갱신작업  
        localStorage.removeItem(todoItem.item);
        localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
      },
    }
  }
</script>

<style scoped>
ul{
  list-style-type: none;
  padding-left: 0;
  margin-top: 0;
  text-align: left;
}
li{
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: #fff;
  border-radius: 5px;
}
.removeBtn{
  margin-left: auto;
  color: #de4343;
}
.checkBtn{
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.checkBtnCompleted {
  color: #b3adad;
}
.textCompleted{
  text-decoration: line-through;
  color: #b3adad;
}
</style>