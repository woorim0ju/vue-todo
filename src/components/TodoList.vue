<template>
  <div>
      <ul>
        <!-- 중요 v-for instance특징, 반복문구의 index를 알려준다 -->
        <!-- 클릭 remove event 위하여 todoItem, index(삭제할 해당건)를 메소드에 넘겨준다 -->
        <li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem.item" class="shadow">
          <i class="fas fa-check checkBtn" v-bind:class="{checkBtnCompleted: todoItem.completed}" 
          v @click="toggleComplete(todoItem, index)"></i>
          <!-- 중요 v-bind 클래스 기존의 html 속성중 todoItem.completed값이 true면 textCompleted class가 동작한다 ->class on/off-->
          <span v-bind:class="{textCompleted: todoItem .completed}" v-on:click="toggleComplete(todoItem, index)">{{todoItem.item}} </span>
          <!-- {{todoItem}}으로 출력시 { "completed": false, "item": "dsdasa" } 로 나옴 -> .item 속성접근 -->
          <!-- todoItem,index를 인자로 넣어 넘긴다 -->
          <span v-on:click="removeItem(todoItem, index)" class="removeBtn"><i class="far fa-trash-alt"></i></span>
        </li>
      </ul>
    </div>
</template>

<script>
export default {
  props: ['propsdata'],
  methods:{
      removeItem: function (todoItem, index){
        this.$emit('removeItem', todoItem, index);
      //console.log(todoItem,index);
      },
      toggleComplete: function (todoItem, index) { //eslint-disable-line no-unused-vars
        this.$emit('toggleItem', todoItem, index)
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