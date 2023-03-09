<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodoItem="addOneItem"></TodoInput>
    <TodoList v-bind:propsdata="todoItems"
              v-on:removeItem="removeOneItem"
              v-on:toggleItem="toggleOneItem">
    </TodoList>
    <TodoFooter v-on:clearAll="clearAllItems"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data: function() {
    return {
      todoItems: []
    }
  },
  methods: {
    // 할 일 추가 - 하위 컴포넌트 -> 상위 컴포넌트 (TodoInput.vue -> App.vue)
    addOneItem: function(todoItem) {
      let obj = {completed: false, item: todoItem};
      localStorage.setItem(todoItem, JSON.stringify(obj));
      this.todoItems.push(obj);
    },
    // 할 일 삭제 - 하위 컴포넌트 -> 상위 컴포넌트 (TodoList.vue -> App.vue)
    removeOneItem: function (todoItem, index) {
      localStorage.removeItem(todoItem.item); // 로컬 스토리지 삭제
      this.todoItems.splice(index, 1); // 로컬 스토리지 내부 뷰 변수 삭제
    },
    // 할 일 완료 - 하위 컴포넌트 -> 상위 컴포넌트 (TodoList.vue -> App.vue)
    toggleOneItem: function (todoItem, index) {
      this.todoItems[index].completed = !this.todoItems[index].completed;
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    // 할 일 지우기 - 하위 컴포넌트 -> 상위 컴포넌트 (TodoFooter.vue -> App.vue)
    clearAllItems: function () {
      localStorage.clear();
      this.todoItems = [];
    }
  },
  created: function () {
    // 로컬 스토리지에 저장된 데이터가 있는 경우, todoItems 배열에 저장
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
          this.todoItems.push(JSON.stringify(localStorage.getItem(localStorage.key(i))));
        }
      }
    }
  },
  components: {
    // 컴포넌트 태그명 : 컴포넌트 내용
    'TodoHeader': TodoHeader,
    'TodoInput': TodoInput,
    'TodoList': TodoList,
    'TodoFooter': TodoFooter
  }
}
</script>

<style>
  body {
    text-align: center;
    background-color: #F6F6F8;
  }
  input {
    border-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03)
  }
</style>
